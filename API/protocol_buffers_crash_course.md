# Protocol Buffers #
1. It is a method for serializing structured data useful for transmitting data over the wire or storing it on the disk.

## Task ##
1. Build an application using pure JSON
2. Re-build the same application using Protocol Buffers
3. Compare the results
	1. In the context of storage
		1. Size of the messages
		2. ...
4. Pros and Cons of protocol buffers

## Details ##
1. Protocol buffer: Message format
2. How do we usually do things
	1. VS Code:
		1. Open
			1. protocobuf (folder)
		2. index.js
			1. Code:
			
					const fs = require("fs");
					const employees = []
					
					employee.push({
						"name": "Hussein",
						"Salary": 1000,
						"id": 1001
					});
					
					const ahmed = {
						"name": "Ahmed",
						"Salary": 9000,
						"id": 1002
					};
					
					employees.push(ahmed);
					
					employee.push({
						"name": "Rick",
						"Salary": 5000,
						"id": 1003
					});
					
					console.log(JSON.stringify(employees));
					
					fs.writeFileSync("jsondata.json", JSON.stringify(employees));
		3. `npm init -y`
		4. How big is the JSON file?
			1. `ls -lh`
				1. ~ 125B
					1. Only for 3 employees (1250B for 30 employees and 125000B ~ 125KB for 3000 employees)
						1. If we send this data on wire, it is large
	2. VS Code:
		1. With protocol buffer (Protocol is structured because it has a schema but JSON doesn't have a schema)
		2. employees.proto (Search marketplace and install vscode-proto3)
		
				syntax = "proto3"; // version 3 of the protocol
				
				message Employee {
					int32 id = 1; // serialization sequence (position of where it is in the message)
					string name = 2;
					float salary = 3;
				}
				
				message Employees {
					repeated Employee employees = 1; // we want as many as possible
				}
				
			1. It is just just a schema definition of the structured data
			2. We are responsible, based on the language of choice, to convert the proto file into a JS file that builds the classes called `Employee` and `Employees` with properties
				1. `protoc` - protocol buffer compiler
					1. Takes the input file and the output langauge
						1. Output language:
							1. Python
							2. C++
							3. Java
							4. JavaScript
					2. Go to: [https://github.com/protocolbuffers/protobuf/releases](https://github.com/protocolbuffers/protobuf/releases)
						1. Find protoc for the OS
							1. Add `protoc` to the PATH variable
					3. Generate JavaScript code:
					
							protoc --js_out=import_style=commonjs,binary:. employees.proto
							
						1. Generates: `employees_pb.js`
				2. Install google-protobuf (runtime)
				
						npm install google-protobuf
				
		3. index2.js
		
				const Schema = require("./employees_pb");
				const fs = require("fs");
				
				const hussein = new Schema.Employee();
				hussein.setId(1001);
				hussein.setName("Hussein");
				hussein.setSalary(1000);
				
				const ahmed = new Schema.Employee();
				ahmed.setId(1002);
				ahmed.setName("Ahmed");
				ahmed.setSalary(9000);
				
				const rick = new Schema.Employee();
				rick.setId(1003);
				rick.setName("Rick");
				rick.setSalary(5000);
				
				const employees = new Schema.Employees();
				employees.addEmployees(hussein);
				employees.addEmployees(ahmed);
				employees.addEmployees(rick);
				
				const bytes = employees.serializeBinary();
				console.log("Binary: " + bytes);
				fs.writeFileSync("employeesbinary", bytes);
				
				const employees2 = Schema.Employees.deserializeBinary(bytes);
				console.log(employees2.toString());
				
			1. Serialize to binary because we send binary over wire
			2. Run the program
				1. Size of binary file: `ls -lh`
					1. ~ 52B  as compared to ~ 125B
						1. Less storage
						2. Less data to transfer on wire
						
## Pros and Cons ##
1. Pros:
	1. Has a schema
		1. Enables many optimizations
			1. To store them efficiently
			2. To encode them efficiently
		2. Less errors
	2. Compact
		1. Small memory footprint
		2. Small disk footprint
		3. Small network footprint
		4. HTTP2 has a compression which will make it even smaller
	3. Language neutral
		1. The proto format is common and agreeable to many language developers
		2. Google took upon themselves to build the compiler to spit out server and client proxy code in the language of our choice
2. Cons:
	1. Development time:
		1. Takes longer time comparitively
		2. The generated code might have bugs
	2. Needs recompilation of proto file if
		1. There are security patches
		2. There are updates
		3. There are bug fixes
		4. It might break the client code
	3. Forced to have a schema
		1. Some people don't like schema
		2. Small applications might not need a schema and schema might be an overkill
		3. Additional files need to be maintained and generated code needs to be maintained