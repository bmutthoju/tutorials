DB Normalization:
1. **First Normal Form (1NF)**
	1. Using row order to convey information is not permitted
	2. Mixing data types within the same column is not permitted
	3. Having a table without a primary key is not permitted
	4. Repeating groups are not permitted
2. **Second Normal Form (2NF)**
	1. Each non-key attribute in the table must be dependent on the entire primary key
		1. Formal definition:
			1. We can't have a non-prime attribute that depends on part of a candidate key
				1. Prime attribute: an attribute that belongs to at least one candidate key
					1. Non-prime attribute: an attribute that doesn't belong to any candidate key
				2. Candidate key: an attribute (or combination of attributes) that uniquely identifies a row in the table
3. **Third Normal Form (3NF)**
	1. Each non-key attribute in the table must depend on the key, the whole key, and nothing but the key
		1. Formal definition:
			1. Each non-prime attribute in a table should depend on every candidate key; it should never depend on part of a candidate key; and it should never depend on other non-prime attributes.
4. **Boyce-Codd Normal Form (BCNF)**
	1. Each attribute in the table must depend on the key, the whole key, and nothing but the key (a candidate key)
		1. Formal definition:
			1. With the exception of trivial functional dependencies (key -> key, key -> {key, attribute, ...}), every functional dependency in a table must be a dependency on a superkey (a candidate key or a superset of a candidate key ({candidate_key, attribute, ...}))
5. **Fourth Normal Form (4NF)**
	1. The only kinds of multivalued dependency allowed in a table are multivalued dependencies on the key
6. **Fifth Normal Form (5NF)**
	1. It must not be possible to describe the table as being the logical result of joining some other tables together