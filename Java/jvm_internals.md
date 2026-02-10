## Teach me - JVM Overview ##

Alright — let’s dive into the **JVM overview** step-by-step so you truly understand how Java works under the hood.

---

## 1️⃣ What is the JVM?

**JVM** stands for **Java Virtual Machine**.
It’s the **runtime engine** that runs Java bytecode — like an interpreter between your Java code and the actual machine (OS + hardware).

You can think of the JVM as:

* **Platform-independent executor** → same Java bytecode runs on Windows, Mac, Linux without recompiling.
* **Memory manager** → allocates, uses, and cleans up memory for your Java program.
* **Performance optimizer** → uses techniques like **JIT (Just-In-Time)** compilation.

---

## 2️⃣ JVM Workflow (Step-by-Step)

When you run a Java program:

1. **You write** Java source code → `.java` file.
2. **Javac compiler** converts it into **bytecode** → `.class` file.
3. **JVM loads** the `.class` file into memory using the **Class Loader**.
4. **Execution Engine** runs the bytecode:

   * Interprets it (line by line) OR
   * Compiles hot code paths to machine code via **JIT** for speed.
5. **Garbage Collector (GC)** cleans up unused objects automatically.

---

## 3️⃣ JVM Architecture

Here’s the high-level structure:

```
                ┌────────────────────────────┐
                │      Class Loader          │
                └───────────┬────────────────┘
                            ↓
                ┌────────────────────────────┐
                │   Runtime Data Areas       │
                │  (Memory)                  │
                │  - Heap                    │
                │  - Stack                   │
                │  - Method Area             │
                │  - PC Register             │
                │  - Native Method Stack     │
                └───────────┬────────────────┘
                            ↓
                ┌────────────────────────────┐
                │    Execution Engine        │
                │  - Interpreter             │
                │  - JIT Compiler            │
                │  - Garbage Collector       │
                └────────────────────────────┘
```

---

## 4️⃣ Components in Detail

### **A. Class Loader**

* Loads `.class` files into the JVM.
* Follows a **parent delegation model** (Bootstrap → Extension → Application class loaders).

### **B. Runtime Data Areas (Memory)**

* **Heap** → Stores objects (shared across threads).
* **Stack** → Stores local variables and method calls (per thread).
* **Method Area** → Stores class metadata, static variables.
* **PC Register** → Keeps track of the current instruction for each thread.
* **Native Method Stack** → Stores native (non-Java) method info.

### **C. Execution Engine**

* **Interpreter** → Reads bytecode line-by-line (slower).
* **JIT Compiler** → Converts frequently executed bytecode (“hot code”) to native machine code (faster).
* **Garbage Collector (GC)** → Frees up unused object memory.

---

## 5️⃣ JVM vs JRE vs JDK

* **JVM** → Runs bytecode (part of JRE).
* **JRE** (Java Runtime Environment) → JVM + libraries to run programs.
* **JDK** (Java Development Kit) → JRE + tools like `javac` for development.

---

## 6️⃣ Why FAANG cares about JVM knowledge

In interviews, JVM topics often pop up in:

* **Performance tuning** (GC tuning, memory leaks)
* **Concurrency issues** (Java Memory Model, thread safety)
* **Debugging production issues** (heap dump, thread dump analysis)

---

If you want, I can now teach you **"Java Memory Model"** next, which is a natural follow-up to JVM overview and extremely important for FAANG-level Java roles.
That’s where concurrency, thread visibility, and ordering guarantees come into play.

Do you want me to go there next?

## Yes, please ##

```java
/*
 * CustomClassLoader_Java17.java
 * Example of a simple custom ClassLoader for modern JVMs (Java 17+ / 21).
 *
 * This file contains:
 *  - A CustomClassLoader that loads .class files from a directory (plugins/)
 *  - A demonstration of loading a class by name and invoking a method via reflection
 *  - Notes and best practices in comments
 *
 * How to use:
 * 1. Compile a simple target class (e.g., Plugin.java) into the plugins/ directory.
 *    Example Plugin.java:
 *      public class Plugin {
 *          public void run() { System.out.println("Hello from Plugin!"); }
 *      }
 *
 * 2. javac -d plugins Plugin.java
 * 3. Compile this file: javac CustomClassLoader_Java17.java
 * 4. Run: java CustomClassLoader_Java17
 *
 * Security / Modules note:
 * - On Java 9+ with strong encapsulation, reflective access to non-exported members may be blocked
 *   unless modules are opened. Loading top-level classes from the classpath or from independent
 *   directories are usually fine; problems arise when trying to access internal JDK classes.
 */

import java.io.IOException;
import java.lang.reflect.Method;
import java.nio.file.Files;
import java.nio.file.Path;
import java.nio.file.Paths;
import java.util.Objects;

public class CustomClassLoader_Java17 {

    /**
     * Simple ClassLoader that loads .class files from a specified directory.
     * It follows parent-delegation by default (doesn't override loadClass).
     * To bypass delegation (isolate classes), you can call new CustomClassLoader(dir, null)
     * which uses the bootstrap loader as a parent.
     */
    public static class DirectoryClassLoader extends ClassLoader {
        private final Path classesRoot;

        /**
         * @param classesRoot directory where .class files are located (absolute or relative)
         * @param parent optional parent class loader; if null, bootstrap loader is used
         */
        public DirectoryClassLoader(Path classesRoot, ClassLoader parent) {
            // delegate to specified parent (can be null)
            super(parent);
            Objects.requireNonNull(classesRoot, "classesRoot cannot be null");
            this.classesRoot = classesRoot;
        }

        /**
         * Converts a binary class name to a file path and loads bytes.
         * Example: com.example.Plugin -> classesRoot/com/example/Plugin.class
         */
        @Override
        protected Class<?> findClass(String name) throws ClassNotFoundException {
            // convert name to path
            String relPath = name.replace('.', '/') + ".class";
            Path classFile = classesRoot.resolve(relPath);

            if (!Files.exists(classFile)) {
                throw new ClassNotFoundException("Class file not found: " + classFile);
            }

            try {
                byte[] classBytes = Files.readAllBytes(classFile);

                // definePackage: optional — define package to avoid IllegalArgumentException later
                int lastDot = name.lastIndexOf('.');
                if (lastDot != -1) {
                    String pkgName = name.substring(0, lastDot);
                    Package pkg = getPackage(pkgName);
                    if (pkg == null) {
                        // definePackage parameters can be null or empty when unknown
                        definePackage(pkgName, null, null, null, null, null, null, null);
                    }
                }

                // defineClass links the bytes into the JVM and returns the Class<?>
                Class<?> defined = defineClass(name, classBytes, 0, classBytes.length);

                // resolveClass is optionally called by loadClass, but here we can resolve explicitly
                resolveClass(defined);
                return defined;
            } catch (IOException e) {
                throw new ClassNotFoundException("Failed to load class bytes for " + name, e);
            }
        }

        /**
         * Optional: override getResourceAsStream / getResource to expose resources from classesRoot.
         */
    }


    // --- Demonstration harness ---
    public static void main(String[] args) throws Exception {
        // Directory where plugin .class files exist (relative to working directory)
        Path pluginDir = Paths.get("plugins").toAbsolutePath();

        System.out.println("Plugins dir: " + pluginDir);

        // Parent delegation example: use system class loader as parent
        ClassLoader parent = ClassLoader.getPlatformClassLoader();
        DirectoryClassLoader loader = new DirectoryClassLoader(pluginDir, parent);

        // Name of the target class to load (binary name)
        String targetClassName = "Plugin"; // or include package: "com.example.Plugin"

        // loadClass uses parent delegation by default: parent will be asked first
        // If the parent cannot find it, JVM will call our findClass implementation.
        Class<?> pluginClass = loader.loadClass(targetClassName);

        System.out.println("Loaded class: " + pluginClass + " with loader: " + pluginClass.getClassLoader());

        // Instantiate and invoke
        Object pluginInstance = pluginClass.getDeclaredConstructor().newInstance();
        Method runMethod = pluginClass.getMethod("run");
        runMethod.invoke(pluginInstance);

        // Demonstrate isolation: if you create another DirectoryClassLoader instance pointing to the same
        // directory but with bootstrap parent (null), classes will be loaded by a different loader and
        // will be != to previous Class<?> objects.
        DirectoryClassLoader isolated = new DirectoryClassLoader(pluginDir, null);
        Class<?> pluginClass2 = isolated.loadClass(targetClassName);

        System.out.println("Loaded by isolated loader: " + (pluginClass2 == pluginClass ? "SAME" : "DIFFERENT"));
        System.out.println("pluginClass loader: " + pluginClass.getClassLoader());
        System.out.println("pluginClass2 loader: " + pluginClass2.getClassLoader());

        // Note: casting between instances loaded by different class loaders will fail with ClassCastException.
        try {
            Object casted = pluginClass.cast(pluginInstance); // fine
            // pluginClass2.cast(pluginInstance); // would throw ClassCastException if uncommented
        } catch (ClassCastException cce) {
            System.err.println("ClassCastException: " + cce.getMessage());
        }
    }

}
```

## Interview-ready walkthrough ##

Nice — let’s build a **practical, interview-ready** walkthrough for writing a **custom class loader** in modern Java (Java 17/21). I’ll explain the key APIs, show a safe, minimal example that loads `.class` files from a directory (and a variant that loads from an in-memory `byte[]`), cover parent-delegation and how to *break* it, and list important pitfalls (modules, security, memory leaks, reloading). Ready? Let’s go.

---

# 1 — Quick recap: methods you need to know

* `ClassLoader#loadClass(String name)` — public entry point that implements the **parent-delegation** model (calls parent first). Usually you don't override this.
* `ClassLoader#findClass(String name)` — override this to *provide* a class; `loadClass` will call it if parent cannot load the class.
* `defineClass(String name, byte[] b, int off, int len)` — converts class bytes to a `Class<?>` object.
* `resolveClass(Class<?> c)` — links the class (optional, `loadClass` typically calls it).
* `findResource(...)`, `findResources(...)`, `getResourceAsStream(...)` — resource lookup override points.
* `close()` (if subclassing a Closeable loader like `URLClassLoader`) — to release native handles.

---

# 2 — Minimal, safe custom loader (loads `.class` from folder)

This example *respects parent delegation* and loads classes whose `.class` file is present in a given directory.

```java
import java.io.IOException;
import java.io.InputStream;
import java.nio.file.Files;
import java.nio.file.Path;
import java.nio.file.Paths;

public class DirectoryClassLoader extends ClassLoader {
    private final Path classesRoot; // root directory where .class files live

    public DirectoryClassLoader(Path classesRoot, ClassLoader parent) {
        super(parent); // pass parent to keep delegation
        this.classesRoot = classesRoot;
    }

    @Override
    protected Class<?> findClass(String name) throws ClassNotFoundException {
        // convert package name to path
        String relativePath = name.replace('.', '/') + ".class";
        Path classFile = classesRoot.resolve(relativePath);

        if (!Files.exists(classFile)) {
            throw new ClassNotFoundException(name);
        }

        try {
            byte[] bytes = Files.readAllBytes(classFile);
            // define class (no protection domain specified here)
            Class<?> c = defineClass(name, bytes, 0, bytes.length);
            // optional: resolveClass(c);
            return c;
        } catch (IOException e) {
            throw new ClassNotFoundException("Failed to load class " + name, e);
        }
    }
}
```

Usage:

```java
Path root = Paths.get("/path/to/classes"); // contains com/example/Hello.class
ClassLoader parent = ClassLoader.getSystemClassLoader();
DirectoryClassLoader loader = new DirectoryClassLoader(root, parent);

Class<?> helloClass = loader.loadClass("com.example.Hello");
Object instance = helloClass.getDeclaredConstructor().newInstance();
helloClass.getMethod("sayHello").invoke(instance);
```

---

# 3 — Loading from in-memory `byte[]` (e.g., dynamic generation, decrypting JAR)

If you get class bytes from network, a DB, or decrypt them first, the main difference is you already have `byte[]`:

```java
@Override
protected Class<?> findClass(String name) throws ClassNotFoundException {
    byte[] bytes = obtainClassBytesSomehow(name); // decrypt/read
    if (bytes == null) throw new ClassNotFoundException(name);
    return defineClass(name, bytes, 0, bytes.length);
}
```

---

# 4 — Parent delegation vs breaking delegation

**Default (safe)** behavior: `loadClass` calls parent first. This prevents replacing JDK/core classes.

If you override `loadClass` and skip delegation, you create a loader that can shadow system classes (dangerous, but sometimes used in plugin systems). Example to *break* delegation:

```java
@Override
public Class<?> loadClass(String name, boolean resolve) throws ClassNotFoundException {
    // try to find locally first (non-delegating)
    synchronized (getClassLoadingLock(name)) {
        Class<?> c = findLoadedClass(name);
        if (c == null) {
            try {
                c = findClass(name); // local
            } catch (ClassNotFoundException e) {
                c = getParent().loadClass(name); // fallback
            }
        }
        if (resolve) resolveClass(c);
        return c;
    }
}
```

**Warning:** Breaking delegation can cause security holes, duplicate core class definitions, `LinkageError`, or `ClassCastException` (two separate class objects with same name but different loaders are incompatible).

---

# 5 — Class identity and isolation (important interview point)

`Class` identity is `(fully-qualified-name, definingClassLoader)`. So:

* `com.example.Foo` loaded by loader A and loader B are *different classes*.
* Instances cannot be cast across those loaders without shared types loaded by a common parent.

This is how application servers isolate webapps / plugin frameworks implement sandboxing.

---

# 6 — Hot reloading (simple pattern)

To reload a class at runtime:

1. Create a *new instance* of your custom ClassLoader (loader1).
2. Load class `X` with loader1.
3. Discard references to classes + loader1 (stop threads started by loaded code).
4. Create loader2 and load new class bytes for `X`.

Because class identity ties to loader, loader2 produces distinct `Class` object and you can use updated code.

Pitfalls: if loader1 or classes it loaded still referenced (static fields, running threads), GC won’t collect them → memory leak.

---

# 7 — Modules (Java 9+) — extra gotchas

* Java 9+ uses the module system (JPMS). If your loaded class tries to reflectively access JDK internals, strong encapsulation may block it unless the module is opened (`--add-opens`) or the target module exports the package.
* Custom class loaders still work for plain classpath-style classes, but loading classes that belong to named modules (e.g., types from `java.base`) is managed by module system — you won’t replace those.
* If you want to load code as a module, you must interact with `java.lang.Module` APIs (e.g., `ModuleLayer`, `Configuration`) — more complex than simple ClassLoader use.

---

# 8 — Security considerations

* Historically the SecurityManager could restrict classloader behavior. SecurityManager is deprecated/removed in later Java — still be careful about loading untrusted code.
* Validate/desanitize class bytes before defineClass (e.g., use bytecode verifier libraries) if loading untrusted code.

---

# 9 — Memory leaks & resource management

Common causes of classloader leaks:

* Threads started by loaded code that remain alive and reference classes (thread’s context classloader).
* Static caches holding references to classes or classloader objects.
* Native libraries loaded by classes (JNI) can pin the classloader.
  Mitigations:
* Provide a lifecycle: stop threads, clear static caches, call `close()` if using `URLClassLoader`.
* Avoid long-lived static references to classes from the loaded classes.

---

# 10 — Resource loading APIs

If your loader packages resources (properties, configs), implement:

```java
@Override
public InputStream getResourceAsStream(String name) {
    // resolve via findResource(name) or custom path
}
```

Note: `Class.getResourceAsStream` uses the defining class loader of the class that invoked it.

---

# 11 — Example: plugin loader skeleton (with isolation + lifecycle)

```java
public class PluginClassLoader extends ClassLoader implements AutoCloseable {
    private final Path root;

    public PluginClassLoader(Path root, ClassLoader parent) {
        super(parent);
        this.root = root;
    }

    @Override
    protected Class<?> findClass(String name) throws ClassNotFoundException {
        try {
            Path p = root.resolve(name.replace('.', '/') + ".class");
            byte[] bytes = Files.readAllBytes(p);
            return defineClass(name, bytes, 0, bytes.length);
        } catch (IOException e) {
            throw new ClassNotFoundException(name, e);
        }
    }

    @Override
    public void close() {
        // release resources if any (native libs), null references to caches etc.
    }
}
```

To reload plugin:

* `close()` old loader
* ensure no references to classes or threads
* create new `PluginClassLoader` and load fresh classes

---

# 12 — Interview talking points (what to say)

If asked in interview, cover:

* The **delegation model** and why it exists (security, uniqueness of core classes).
* `findClass` + `defineClass` as the canonical extension points.
* Class identity is `(name, loader)` → implications for casting.
* Module system effects (Java 9+): strong encapsulation, `jmod` vs `rt.jar`.
* Hot-reload pattern using new loader instances + GC caveats (leaks).
* Security and resource management (stop threads, close URLClassLoader).

---

# 13 — Quick FAQ

Q: *Can I modify an existing class definition in place?*
A: Not with standard ClassLoader APIs. Once a `Class` is defined, it can't be redefined by the same loader except via JVM tooling (`Instrumentation#redefineClasses`) or JVM debug agents.

Q: *When should I override `loadClass`?*
A: Rarely — only when you really need non-delegating semantics (plugin sandbox, version isolation). Default `findClass` override is safer.

Q: *How to load classes packaged inside a JAR?*
A: Use `URLClassLoader` (or `java.net` APIs) to point at the JAR URL and rely on `findResource` / `getResourceAsStream`, or read JAR entries and `defineClass` manually.

---

If you want, I can:

* Show a **full runnable demo** project that (a) compiles a tiny class at runtime, (b) loads it with a custom loader from bytes, (c) demonstrates reloading and the `ClassCastException` that occurs across loaders.
* Or show **how to load classes from a JAR** using `URLClassLoader` (and how to close it properly).

Which of those would you like next?

## Show how to load classes from a JAR using URLClassLoader. ##

Alright — let’s walk through a **hands-on example** of loading classes dynamically from a JAR using `URLClassLoader` in **modern Java** (Java 17+).

> Note: `URLClassLoader` is **still available** but marked as *not recommended for new code* in some cases — however, it’s fine for plugin loading or interview demos.

---

## **1️⃣ Project Setup**

We’ll have:

* `plugin.jar` → contains a class `com.example.Plugin` with a method `run()`.
* `MainApp` → loads that class from the JAR **at runtime**, without compile-time dependency.

---

## **2️⃣ Plugin Code (to be packaged into a JAR)**

**`src/com/example/Plugin.java`**

```java
package com.example;

public class Plugin {
    public void run() {
        System.out.println("Plugin is running!");
    }
}
```

Compile and create the JAR:

```bash
javac -d out src/com/example/Plugin.java
jar cf plugin.jar -C out .
```

---

## **3️⃣ Loader Code Using `URLClassLoader`**

**`MainApp.java`**

```java
import java.io.File;
import java.lang.reflect.Method;
import java.net.URL;
import java.net.URLClassLoader;

public class MainApp {
    public static void main(String[] args) throws Exception {
        // Path to your JAR
        File jarFile = new File("plugin.jar");
        URL jarURL = jarFile.toURI().toURL();

        // Create a new class loader with the JAR
        try (URLClassLoader loader = new URLClassLoader(new URL[]{jarURL}, MainApp.class.getClassLoader())) {
            
            // Load the class by name
            Class<?> pluginClass = loader.loadClass("com.example.Plugin");
            
            // Create an instance
            Object pluginInstance = pluginClass.getDeclaredConstructor().newInstance();
            
            // Call the 'run' method using reflection
            Method runMethod = pluginClass.getMethod("run");
            runMethod.invoke(pluginInstance);
        }
    }
}
```

---

## **4️⃣ Running It**

```bash
javac MainApp.java
java MainApp
```

Output:

```
Plugin is running!
```

---

## **5️⃣ How It Works Internally**

1. `URLClassLoader` reads the `plugin.jar` file.
2. It parses the JAR manifest and indexes `.class` entries.
3. When `loadClass` is called:

   * Delegates to **parent class loader** first.
   * If not found, reads the `.class` bytes from the JAR.
   * Calls `defineClass()` to turn bytes into a JVM `Class` object.
4. The class is **verified, prepared, resolved, and initialized**.
5. Reflection is used to create an object and invoke methods.

---

## **6️⃣ FAANG-Relevant Extensions**

* **Hot swapping**: Keep the `URLClassLoader` in a separate thread, close it, and reload JARs for updates without restarting.
* **Sandboxing**: Use a custom subclass of `ClassLoader` to restrict what packages can be loaded.
* **Service Loader**: Combine with `java.util.ServiceLoader` for plugin discovery without hardcoding class names.

---

If you want, I can now show you **how to write your own ClassLoader from scratch** (no `URLClassLoader`) so you see exactly how `defineClass()` works under the hood — that’s an advanced FAANG-level interview question.

Do you want me to go there next?

## Yes, please ##

Alright — let’s go full deep dive and **write our own ClassLoader from scratch**, without relying on `URLClassLoader`.

This is an **FAANG-level** topic because it touches:

* JVM class loading internals
* `defineClass()`
* Delegation model
* Security & isolation

---

## **1️⃣ Understanding the Goal**

We’ll:

* Create a JAR (or `.class` file) separately.
* Write a **custom ClassLoader** that:

  * Reads the `.class` file as bytes.
  * Converts bytes → `Class<?>` via `defineClass()`.
  * Loads and runs a method from it.

---

## **2️⃣ Plugin Code (Same as before)**

`Plugin.java` (to be loaded dynamically)

```java
package com.example;

public class Plugin {
    public void run() {
        System.out.println("Plugin loaded by custom ClassLoader!");
    }
}
```

Compile:

```bash
javac -d out Plugin.java
```

We now have:

```
out/com/example/Plugin.class
```

---

## **3️⃣ Custom ClassLoader Implementation**

`CustomClassLoader.java`

```java
import java.io.IOException;
import java.nio.file.Files;
import java.nio.file.Path;

public class CustomClassLoader extends ClassLoader {

    private final Path classesDir;

    public CustomClassLoader(Path classesDir) {
        // Pass null to avoid parent delegation for demonstration
        super(CustomClassLoader.class.getClassLoader()); 
        this.classesDir = classesDir;
    }

    @Override
    protected Class<?> findClass(String name) throws ClassNotFoundException {
        try {
            // Convert class name to file path
            String fileName = name.replace('.', '/') + ".class";
            Path classFile = classesDir.resolve(fileName);

            // Read bytes
            byte[] classBytes = Files.readAllBytes(classFile);

            // Define the class in JVM
            return defineClass(name, classBytes, 0, classBytes.length);
        } catch (IOException e) {
            throw new ClassNotFoundException("Could not load " + name, e);
        }
    }
}
```

---

## **4️⃣ Loader App Using the Custom ClassLoader**

`MainApp.java`

```java
import java.lang.reflect.Method;
import java.nio.file.Path;

public class MainApp {
    public static void main(String[] args) throws Exception {
        Path pluginDir = Path.of("out"); // folder with Plugin.class

        CustomClassLoader loader = new CustomClassLoader(pluginDir);

        // Load class without compile-time dependency
        Class<?> pluginClass = loader.loadClass("com.example.Plugin");

        // Create instance
        Object pluginInstance = pluginClass.getDeclaredConstructor().newInstance();

        // Invoke run()
        Method runMethod = pluginClass.getMethod("run");
        runMethod.invoke(pluginInstance);

        System.out.println("Loaded by: " + pluginClass.getClassLoader());
    }
}
```

---

## **5️⃣ Running It**

```bash
javac CustomClassLoader.java MainApp.java
java MainApp
```

Output:

```
Plugin loaded by custom ClassLoader!
Loaded by: CustomClassLoader@<hashcode>
```

---

## **6️⃣ What’s Happening Internally**

1. **`loadClass()`** in `ClassLoader`:

   * Calls `findLoadedClass()` (checks if already loaded).
   * Delegates to **parent loader** (by default).
   * If parent fails → calls `findClass()` in your loader.
2. In our override of `findClass()`:

   * We read raw bytes from disk.
   * Call `defineClass()` — this:

     * **Verifies** bytecode.
     * Allocates JVM metadata for the class.
     * Links methods/fields to the runtime constant pool.
     * Marks the class as loaded in your loader’s namespace.
3. The class is now ready for instantiation and method calls.

---

## **7️⃣ FAANG Interview Angles**

* **ClassLoader isolation** → Different loaders can load the *same* class name without conflict.
* **Hot reload** → Create a new instance of the loader each time you want a fresh version.
* **Security** → Restrict package loading (override `loadClass` and block dangerous packages).
* **Parent-first vs Child-first** loading → Useful for overriding system classes in frameworks.

---

If you want, I can next show you a **diagram of the JVM class loading lifecycle** (Loading → Linking → Initialization) and how **custom class loaders** fit into the delegation hierarchy — that’s the visual most interviewers love.

Do you want me to draw that next?
