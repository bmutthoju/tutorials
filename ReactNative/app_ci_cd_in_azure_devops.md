## How to set up Azure DevOps for iOS and Android app build, deployment, and delivery? ##

Setting up **Azure DevOps** for iOS and Android app build, deployment, and delivery involves configuring CI/CD pipelines that automate building, testing, and publishing your apps. I’ll break it down step by step for **both platforms**:

---

## 1. **Pre-requisites**

* **Azure DevOps account** → [https://dev.azure.com](https://dev.azure.com)
* **Code repository** → GitHub, Bitbucket, or Azure Repos
* **Apple Developer Account** (for iOS signing, provisioning profiles, and App Store deployment)
* **Google Play Developer Account** (for Android release delivery)
* **App Center account** (optional, for app distribution and crash analytics)

---

## 2. **Create an Azure DevOps Project**

1. Go to [Azure DevOps](https://dev.azure.com).
2. Create a new **project** (choose Git if using Azure Repos).
3. Import or push your **mobile app code** (Flutter, React Native, Xamarin, Native, etc.) into the repo.

---

## 3. **Service Connections**

* **For iOS**:

  * Create a **Service Connection** for **Apple App Store Connect** (Service Principal with App Store API Key).
  * Upload certificates (.p12) and provisioning profiles, or use **Secure Files** in DevOps.

* **For Android**:

  * Create a **Service Connection** for **Google Play** (upload the `service-account.json` from Google Play Console).

---

## 4. **Pipeline Setup**

You can use **YAML pipelines** or **Classic UI pipelines**. YAML is preferred for versioning.

### Example: **iOS Pipeline (Xcode)**

```yaml
trigger:
- main

pool:
  vmImage: 'macos-latest'

steps:
- task: InstallAppleCertificate@2
  inputs:
    certSecureFile: 'ios_distribution.p12'
    certPwd: '$(P12Password)'

- task: InstallAppleProvisioningProfile@1
  inputs:
    provisioningProfileLocation: 'secureFiles'
    provProfileSecureFile: 'MyApp.mobileprovision'

- task: Bash@3
  inputs:
    targetType: 'inline'
    script: |
      pod install
      xcodebuild -workspace MyApp.xcworkspace \
        -scheme MyApp \
        -sdk iphoneos \
        -configuration Release \
        archive -archivePath build/MyApp.xcarchive

- task: Xcode@5
  inputs:
    actions: 'export'
    exportPath: 'build'
    exportOptions: 'plist'
    exportOptionsPlist: 'ExportOptions.plist'

- task: AppStoreRelease@1
  inputs:
    serviceEndpoint: 'AppleServiceConnection'
    appIdentifier: 'com.example.myapp'
    ipaPath: 'build/MyApp.ipa'
    releaseTrack: 'TestFlight'
```

---

### Example: **Android Pipeline (Gradle)**

```yaml
trigger:
- main

pool:
  vmImage: 'ubuntu-latest'

steps:
- task: Gradle@2
  inputs:
    workingDirectory: ''
    gradleWrapperFile: 'gradlew'
    gradleOptions: '-Xmx3072m'
    publishJUnitResults: true
    jdkVersionOption: 11
    tasks: 'assembleRelease'

- task: AndroidSigning@3
  inputs:
    apkFiles: '**/*.apk'
    apksignerKeystoreFile: 'my-keystore.jks'
    apksignerKeystorePassword: '$(KeystorePassword)'
    apksignerKeyAlias: 'mykey'
    apksignerKeyPassword: '$(KeyPassword)'

- task: GooglePlayRelease@4
  inputs:
    serviceConnection: 'GooglePlayServiceConnection'
    applicationId: 'com.example.myapp'
    bundleFile: '**/*.aab'
    track: 'internal'
```

---

## 5. **App Distribution**

* **Internal testing** → distribute to testers via **App Center**, **TestFlight**, or **Google Play Internal Track**.
* **Staging/Production** → push to App Store / Google Play using pipeline tasks.

---

## 6. **Best Practices**

* Store **secrets** (API keys, passwords) in **Azure Key Vault** or **Pipeline Variables** (marked secret).
* Use **stages** (Build → Test → Deploy) in YAML to separate environments.
* Run **unit/UI tests** on pipeline (XCTest, Espresso, Flutter Driver, etc.).
* Use **branches & triggers**:

  * `main` → production release
  * `develop` → internal testing builds

---

✅ With this setup, every **commit/pull request** can trigger builds, and merges to **main** can automatically ship to **TestFlight** (iOS) or **Google Play Internal Track** (Android).

---

Do you want me to create a **combined YAML pipeline** (single file) that handles **both iOS and Android** in one Azure DevOps project?


## Give the steps for Google Play Developer Account. ##

Got it 👍 — here are the **steps to set up a Google Play Developer Account** so you can publish Android apps and connect it with Azure DevOps for CI/CD:

---

## 1. **Sign Up for a Google Play Developer Account**

1. Go to [Google Play Console](https://play.google.com/console).
2. Sign in with your **Google account** (preferably a company or dedicated email, not a personal one).
3. Click **Create account** → choose **Developer account**.
4. Select account type:

   * **Individual** (for a single developer)
   * **Organization** (recommended if you’re a company/startup).
5. Fill in developer profile details:

   * Developer name (publicly visible in Play Store)
   * Contact email, phone, and address

---

## 2. **Pay Registration Fee**

* A **one-time fee of \$25 USD** (non-refundable).
* Pay using a **credit/debit card**.

---

## 3. **Accept Developer Distribution Agreement**

* Read and accept Google Play Developer distribution terms.

---

## 4. **Set Up Payment Profile (Optional but Recommended)**

* If you want to sell paid apps or in-app products:

  * Go to **Play Console → Monetize → Set up Payment Profile**.
  * Provide tax information, banking details, and business info.

---

## 5. **Enable API Access for Automation (For Azure DevOps)**

To connect Azure DevOps pipelines with Google Play for automatic delivery:

1. In **Google Play Console**, go to:
   `Settings → Developer account → API access`
2. Click **Link to Google Cloud Project** (create a new one if you don’t have).
3. In the linked Google Cloud Console:

   * Go to **IAM & Admin → Service Accounts**.
   * Create a **new Service Account**.
   * Assign role: **Release Manager** or **Editor**.
   * Create a JSON key and **download it** (`service-account.json`).
4. Back in Play Console → **API Access** → Grant access to the Service Account.

   * Assign permissions (usually **Release Manager** to upload builds).

---

## 6. **Upload Your First App**

* Go to **All Apps → Create App**.
* Fill in app details (app name, language, free/paid, etc.).
* Complete the following:

  * App Content (privacy policy, data safety, ads declaration)
  * Store Listing (app description, screenshots, icons)
  * App Release (upload `.aab` or `.apk`)
  * Content Rating questionnaire

---

## 7. **Connect with Azure DevOps**

1. In **Azure DevOps**, create a **Service Connection**:

   * Go to **Project Settings → Service Connections → New Service Connection → Google Play**.
   * Upload the **service-account.json** from step 5.
2. Use the `GooglePlayRelease@4` task in your pipeline to publish `.aab` or `.apk` files automatically.

---

✅ After this, you’re ready to publish apps and push new builds via **CI/CD pipelines** in Azure DevOps.

---

Do you want me to also show you how to **create and configure the service connection in Azure DevOps with screenshots/steps** so you can directly link it with your Play Console?

## Yes, please. ##

Perfect 👍 — let me walk you through **step-by-step with details** on how to create and configure a **Google Play Service Connection in Azure DevOps**, so that your pipeline can publish `.aab` or `.apk` directly to the Play Store.

---

## 🔹 Step 1. Prepare Google Play Service Account JSON

This is from the Google Play Console setup we discussed:

1. Go to **Google Play Console → Settings → Developer account → API access**.
2. Link to a **Google Cloud project**.
3. In **Google Cloud Console → IAM & Admin → Service Accounts**:

   * Create a **Service Account** (e.g., `azure-devops-deployer`).
   * Assign **Release Manager** (recommended) or **Editor** role.
   * Generate a **JSON Key** and download it → this file will be named something like:
     `service-account.json`

⚠️ **Keep this JSON file safe**, it contains private credentials.

---

## 🔹 Step 2. Add Service Connection in Azure DevOps

1. Go to your **Azure DevOps Project**.
2. On the left menu, click **Project Settings (⚙️)**.
3. Under **Pipelines**, select **Service connections**.
4. Click **New service connection** → choose **Google Play**.
5. A dialog will appear → upload your **service-account.json** file.
6. Give the connection a name, e.g., `GooglePlayServiceConnection`.
7. Click **Verify and Save** → it should validate successfully.

---

## 🔹 Step 3. Configure Secure Files (Optional, for signing)

If you need to **sign your APK/AAB** before uploading:

1. Go to **Pipelines → Library → Secure Files**.
2. Upload your **keystore file (`.jks`)**.
3. Reference it in your pipeline with the `AndroidSigning@3` task.

---

## 🔹 Step 4. Use Service Connection in Pipeline

Now you can use it in your YAML pipeline:

```yaml
- task: GooglePlayRelease@4
  inputs:
    serviceConnection: 'GooglePlayServiceConnection'
    applicationId: 'com.example.myapp'
    bundleFile: '**/*.aab'   # or use **/*.apk if uploading APK
    track: 'internal'        # internal | alpha | beta | production
```

---

## 🔹 Step 5. Test Deployment

* Run a build → your pipeline should **upload the `.aab` or `.apk`** to the **Google Play Internal track**.
* You can check status in **Google Play Console → Release → App releases**.

---

⚡ Pro Tips:

* Use **Internal Track** for testers → faster uploads, no Play Store review needed.
* Use **Stages in Azure DevOps** → Build → Sign → Deploy (internal → production).
* Store secrets (keystore password, key alias, etc.) in **Pipeline Variables** (marked secret).

---

👉 Do you want me to also prepare a **full working YAML pipeline (end-to-end)** for Android (including build, sign, and deploy), so you can just drop it into your Azure DevOps?
