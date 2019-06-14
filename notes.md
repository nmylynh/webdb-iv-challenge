Introduction to Data Modeling

Data modeling is a game of abstraction.

A good data model:
 -- captures all the data the system needs.
 -- captures ONLY the data the system needs.
 -- reflects reality.
 -- is flexible, and can evolve with the system.
 -- guarantee data integrity without sacrificing performance.
 -- is driven by the way we access data in the system.
 -- optimize last once you have a solid structure.

Components:
 -- entities: the nouns, resources in REST terminology.
 -- properties: information we need to track about the entity.
 -- relationships: how they relate to each other.

Workflow
 -- identify entities.
 -- indentify properties for each entity.
 -- identify relationships between two entities at a time.

Ideally you want to get to the JNF (third normal form).