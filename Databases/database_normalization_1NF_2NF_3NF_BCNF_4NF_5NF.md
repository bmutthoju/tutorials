# Database Normalization - 1NF, 2NF, 3NF, 4NF, 5NF #
## Questions ##
1. What is normalization?
2. Why do we do it?
3. How do we do it?
4. What bad things can happen if we don't do it?

## Topics ##
1. Database normalization from a practical perspective
2. 1NF to 5NF
3. What do we gain by doing normalization
4. What do we lose if we fail to do it

## Data ##
1. Some data is wrong
	1. Good database design cannot protect from much bad data
	2. Good database design can protect from some bad data
		1. Suppose data tells something that cannot logically be true
			1. Example: A customer with two dates of birth (illogical)
			2. Data that fails data integrity:
				1. Data cannot be trusted because it does not agree with itself
					1. It is not only a problem of data but also a bad database design
2. What is normalization?
	1. When we normalize a database table, we structure it in such a way that it cannot express redundant information
		1. In a normalized table, we would not be able to give a customer 2 dates of birth even if we wanted to
	2. A normalized table can express only one version of the truth
3. Advantages of normalized data:
	1. It becomes easier to understand
	2. Easier to enhance and extend
	3. Protected from:
		1. Insertion anomalies
		2. Update anomalies
		3. Deletion anomalies
4. How do we determine if a table is normalized or not?
	1. How do we determine if there is a danger that redundant data can creap into the table?
		1. Solution: There are sets of criteria we can use to assess the level of danger
			1. Criteria:
				1. 1NF
				2. 2NF
				3. 3NF
				4. 4NF
				5. 5NF
	2. Analogy:
		1. Safety assessments:
			1. Bridge:
				1. Safety level 1: Safe for pedestrian traffic
				2. Safety level 2: Safe for cars
					1. Engineer does a stricter assessment of the bridge
				3. Safety level 3: Safe for trucks
	3. Safety assessments for table:
		1. 1NF: Bare minimum safety guarantee
		2. 2NF: Better safety guarantee
		3. ...

## 1NF ##
1. Example: Who are the members of the Beatles?
	1. John, Paul, George, and Ringo
	2. Paul, John, Ringo, and George
		1. The above two are the equivalent (different order is accepted)
	3. Query:
	
			SELECT member_name
			FROM members_of_beatles;
			
		1. The results are returned in an arbitrary order
2. Example: Members of the Beatles from tallest to shortest
	1. Order of names conveys meanings
		1. **This data is not normalized**
			1. **There is no row order in relational database**
				1. **Using row order to convey information violates 1NF**
	2. Solution: Be explicit
		1. Capture height information in a separate column
		
			beatle_height_Ranking
			Beatle	|	Height Ranking
			George	|	3
			Paul	|	1
			Ringo	|	4
			John	|	2
			
		1. Better solution:
		
				beatle_height
				beatle	|	height_in_cm
				George	|	178
				John	|	179
				Ringo	|	170
				Paul	|	180
				
3. **Mixing data types violates 1NF**:

		Beatle_Height
		Beatle	|	Height_In_Cm
		George	|	178
		Ringo	|	Somewhere between 168 and 171
		Paul	|	180
		
	1. We cannot be ambiguous about a column's data-type
		1. Don't mix integers and strings
			1. Once we have decided the type of the column, all values in the column must be of the type
	2. Mixing data types within the same column violates 1NF
		1. (and the DB platform won't let you do it anyway)
4. **Designing a table without primary key violates 1NF**
	1. Primary key is a column or a combination of columns that uniquely identifies a row in a table
		1. Example:
		
				Beatle_Height should tell about one beatle in the table
				
				Beatle	|	Height_In_Cm
				George	|	178
				John	|	179
				Ringo	|	170
				Paul	|	180
				
			1. Beatle column can be the primary key of the table
				1. DB platform needs to know our choice of primary key
					1. Get primary key into the db by doing the following:
					
							ALTER TABLE Beatle_Height
							ADD PRIMARY KEY (Beatle);
							
						1. **Making "Beatle" the primary key prevents this:**
							1. Inserting multiple rows for the same Beatle
								1. Multiple rows can be non-sensical and perhaps contradictory
								
										John: 179
										John: 186
										
	2. **Table without a primary key violates 1NF**
5. **"Repeating groups" violates 1NF**
	1. Example: Online multi-player game

			Player_ID	Inventory
			jdog21		2 amulets, 4 rings
			gila19		18 copper coins
			trev73		3 shields, 5 arrows, 30 copper coins, 7 rings
			
		1. Inventory: repeating group:
			1. Each inventory contains many types of items
				1. There could be 100s
		2. Inventory can be a string of text:
			1. Problem: Terrible design
				1. There is no easy way of querying it
					1. How to fetch players with more than 10 copper coins
						1. Impractical to write a query that gives the answer
			2. A solution:
			
					Player_ID | Quantity_1 | Item_Type_1 | ...
					jdog21    | 2          | amulets     | ...
					gila9     | 18         | copper coins| ...
					trev73    | 3          | shields     | ...
					
				1. A player can have 100s of items
					1. It may be impractical to design a table of 100s of columns
						1. Even if we design a table with 100s of columns, it is impractical
		3. Storing a repeating group of data items on a single row violates 1NF
			1. Solution:
			
					Player_ID | Item_Type   | Item_Quantity
					jdog21      amulets       2
					jdog21      rings         4
					gila19      copper coins  18
					trev73      shields       3
					trev73      arrows        5
					trev73      copper coins  30
					trev73      rings         7
					
				1. Each row tells us about one unique combination of player and item_type
					1. PK: (player, item_type)

### First Normal Form Rules: ###
1. Using row order to convey information is not permitted
2. Mixing data types within the same column is not permitted
3. Having a table without a primary key is not permitted
4. Repeating groups are not permitted

## 2NF ##
1. Consider the Player_Inventory table
	1. Let us assume that each player has rating
		1. beginner, intermediate, or advanced
			1. One solution: Add a column called `Player_Rating`
			
					jdog21 | amulets | 2 | Intermediate
					jdog21 | rings   | 4 | intermediate
					...
					
				1. `jdog21` has two rows and we need to update both rows with `intermediate`
				2. `trev73` has four rows and we need to update all four rows with `Advanced`
				3. Problems with the solution:
					1. If `gila19` loses all `copper coins`, then she will lose her rating
						1. The row is deleted
							1. If we query rating, we don't have that data saved
						2. **deletion anamoly**
		2. If `jdog21` moves from `Intermediate` to `Advanced`
			1. We run an Update
				1. Let us say the update went wrong
					1. By accident only one row has got updated
					
							jdog21 | ... | Intermediate
							jdog21 | ... | Advanced
							
						1. **update anomaly**
		3. If a new player comes along and she is a beginner but she doesn't have anything in her inventory yet
			1. We cannot insert any row for her because she doesn't have any inventory
				1. **insertion anamoly**
	2. The reasons for the anamolies is that the table is not in 2NF
2. What is 2NF?
	1. It is how non-key columns relate to the primary key
		1. non-key columns/attributes:
			1. `Item_Quantity`
			2. `Player_Rating`
		2. The non-key attributes do not belong to the primary key
			1. primary key: {Player_ID, Item_Type}
	2. Informal definition of 2NF:
		1. Each non-key attribute must depend on the entire primary key
			1. Example:
				1. Does `Item_Quantity` depend on primary key?
					1. Yes
						1. It belongs to a specific item of a specific player
						
							{ Player_ID, Item_Type } -> { Item_Quantity }
							
						1. `->` - functional dependency
							1. Each value on the left side of the arrow is exactly associated with only one value on the right side of the arrow
							2. Example: The `Player_Rating` does not depend on the entire primary key
							
									{ Player_ID } -> { Player_Rating }
									
								1. It is a property of a player only
									1. Problem: Payer is not the entire primary key but is a part of the primary key
		2. **If a non-key attribute depends on part of the primary-key but not the whole primary-key, then it violates 2NF**
			1. Solution: `Player_Rating` did not belong in the table
				1. If a non-key attribute depends on a portion of the key, then the portion of the key can be extracted out into another table as a primary key of the table. The non-key attributes that depend on the new primary key can be moved to the new table.
				
						Player
						Player_ID | Player_Rating
						jdog21    | Intermediate
						gila19    | Beginner
						trev73    | Advanced
						tina42    | Beginner
						
						Player_Inventory
						Player_ID | Item_Type | Item_Quantity
						jdog21    | amulets   | 2
						jdog21    | rings     | 4
						gila19    | copper coins | 18
						trev73    | shields   | 3
						trev73    | arrows    | 5
						trev73    | copper coins | 30
						trev73    | rings     | 7
						
					1. **There must not be part-key dependencies**
						1. { Player_ID } -> { Player_Rating }
						2. { Player_ID, Item_Type } -> { Item_Quantity }
					2. **An attribute must depend on the whole primary key and not just part of it**

## 3NF ##
1. Example: Adding a column called `Player_Skill_Level`

		Player_ID | Player_Rating | Player_Skill_Level
		
2. Let us say there is a 9 point scale for skill level
	1. 1 - beginner
	2. 9 - expert
3. Division of rating:
	1. 1 - 3 - beginner
	2. 4 - 6 - intermediate
	3. 7 - 9 - advanced
4. Problem: If `gila19`'s skill level gets updated from 3 to 4
	1. Skill level is updated to 4
	2. Suppose we fail to update `Player_Rating`
		1. Leads to data inconsistency
			1. `Player_Rating` says `Beginner` but `Player_Skill_Level` is 4 (indicating `Intermediate`)
				1. `Player_Skill_Level` and `Player_Rating` are dependent on `Player_ID` (satisfies 2NF)
	3. Dependencies:
	
			{ Player_ID } -> { Player_Skill_Level }
			{ Player_ID } -> { Player_Skill_Level } -> { Player_Rating }
			
		1. Indirect dependency
			1. **A transitive dependency**
				1. **Dependency of a non-key attribute on another non-key attribute violates 3NF**
5. Solution:
	1. Add a new table and use the non-key attribute on which another non-key attribute depends on as the primary key of the table. Move the non-key attributes that depends on the new primary key to the new table
	
			Player
			Player_ID | Player_Skill_Level
			jdog21    | 4
			gila19    | 4
			trev73    | 8
			tina42    | 1
			
			Player_Skill_Levels
			Player_Skill_Level | Player_Rating
			1                  | Beginner
			2                  | Beginner
			3                  | Beginner
			4                  | Intermediate
			5                  | Intermediate
			...
			
		1. 3NF is a combination of everything so far
	2. **Summary of 1NF, 2NF, and 3NF: Every non-key attribute in a table should depend on the key, the whole key, and nothing but the key**
		1. This gives us fully normalized tables 99% of the time
	3. **Boyce-Codd Normal Form: Every attribute in a table should depend on the key, the whole key, and nothing but the key** (not just non-key attributes)
		1. Difference is extremely small
			1. 3NF usually complies with BCNF
				1. Exceptions: Multiple-overlapping candidate keys
6. BCNF is enough usually and the table is fully normalized mostly
7. There are some rare cases that need 4NF and 5NF

## 4NF ##
1. Scenario: Design my bird-house .com
	1. A leading supplier of customized bird-houses
		1. Customer can choose between bird-house models
		2. Customers can choose custom color and styles
		3. Each model has a range of avaialble colors ans styles
	2. How to capture this info?
		1. One solution: Put all combinations in a single table
		
				Model_Colors_And_Styels_Available
				Model  | Color  | Style
				Tweety | Yellow | Bungalow
				Tweety | Yellow | Duplex
				Tweety | Blue   | Bungalow
				Tweety | Blue   | Duplex
				Metro  | Brown  | High-Rise
				Metro  | Brown  | Modular
				Metro  | Grey   | High-Rise
				Metro  | Grey   | Modular
				Praire | Brown  | Bungalow
				Praire | Brown  | Schoolhouse
				Praire | Beige  | Bungalow
				Praire | Beige  | Schoolhouse
				
			1. Everything depends on key, the whole key, and nothing but the key
	3. Problems:
		1. Suppose we introduce a third color for Praire - Green
			1. We need to add 2 more rows to the table
			
					Praire | Green | Bungalow
					Praire | Green | Schoolhouse
					
				1. If by mistake we only add the first row, then we have a data inconsistency
					1. **Available colors must be completely independent of available styles**
						1. Table design issue
		2. Solution:
			1. Does color have functional dependency on model?
				1. No
					1. There is no { Model } -> { Color }
			2. Color seems to have some relationship with model
				1. How to express it?
					1. Each model has a set of available colors (**Called multi-valued dependency**)
					
							{ Model } ->> { Color }
							{ Model } ->> { Style }
							
				2. **4NF: Multivalued dependencies in a table must be multivalued dependencies on the key**
					1. In the above example, `Model` is not the key
						1. Solution: Multiple tables:
						
								Model_Colors_Available
								Model  | Color
								Tweety | Yellow
								Tweety | Blue
								Metro  | Brown
								Metro  | Grey
								Praire | Brown
								Praire | Beige
								Praire | Green
								
								Model_Styles_Available
								Model  | Style
								Tweety | Bungalow
								Tweety | Duplex
								Metro  | High-Rise
								Metro  | Modular
								Praire | Bungalow
								Praire | Schoolhouse
								
							1. No aomalies are possible
							
## 5NF ##
1. 