#📘 Project Title: Designing a Normalized Relational Database for OpenAlex Scholarly Knowledge Graph

📄 Project Description:
This project focuses on designing a robust and normalized Entity-Relationship (ER) model for the OpenAlex dataset—an open catalog of scholarly papers, authors, institutions, concepts, sources (journals/venues), and funders. OpenAlex provides a rich, interconnected knowledge graph of academic metadata. The main objective of this project is to transform this complex, JSON-based dataset into a clean, relational database schema optimized for querying, analysis, and integration with downstream research applications.

📌 Goals and Objectives:
To understand and represent the real-world entities and relationships within the OpenAlex schema (such as papers, authorships, institutions, concepts, etc.)

To apply advanced ER modeling techniques including strong/weak entities, associative entities, multi-valued attributes, and hierarchical relationships.

To perform logical database design, ensuring referential integrity and eliminating redundancy through normalization up to Third Normal Form (3NF).

To build a scalable and query-efficient relational schema that can serve as a backend for research analytics or knowledge discovery systems.


### 🔍 Interactive ER Diagram (Zoomable)

![ER Diagram Preview](https://github.com/Gowtham-AI25/Finance_research_papers_database/blob/main/Finance_research_paper_image.jpg)

[📄 Click here to view interactive ER diagram](https://gowtham-ai25.github.io/Finance_research_papers_database/Finance_research_paper_11.drawio.html)



---

### 🔑 **ER Model Concepts with Real Examples and Column Names (OpenAlex Project)**

1. **Strong Entity**

   * ✅ `meta_data(paper_id, title, abstract, ...)`

     > Core independent entity representing papers.

2. **Weak Entity**

   * ✅ `publisher(paper_id)`

     > Depends on `meta_data.paper_id`, has no separate key of its own.

3. **Associative Entity**

   * ✅ `paper_author(paper_id, author_id, author_role)`

     > Connects papers with authors including relationship metadata.

4. **Composite Key**

   * ✅ `index(paper_id, index_name)`
   * ✅ `references(paper_id, reference_ids)`

     > Combines multiple columns as a primary key.

5. **Surrogate Key**

   * ✅ `author_data.author_id`, `concept_name.concept_id`, `topic_name.topic_id`

     > Arbitrary unique IDs used instead of natural keys.

6. **Recursive Relationship**

   * ✅ You can add `related_concept_id` in `concept_name` to model broader concepts.
     *(Not in current schema but suggested for recursive hierarchy)*


7. **One-to-One (1:1)**

   * ✅ `pmc_table(paper_id)` and `pubmed_table(paper_id)`

     > Each paper can have at most one PMC ID or PubMed ID.

8. **One-to-Many (1\:N)**

   * ✅ `meta_data.paper_id` → `citation`, `publisher`, `openaccess`, etc.

     > Each paper connects to many related facts.

9. **Many-to-Many (M\:N)**

    * ✅ `paper_author(paper_id, author_id)`
    * ✅ `keywords(paper_id, keyword_ids)`

    > Multiple authors per paper and vice versa.

10. **Derived Attribute**

    * ✅ `citation.total_citations`

    > Can be derived by counting `references` or citations received.

11. **Total Participation**

    * ✅ `publisher.paper_id [not null, ref > meta_data.paper_id]`

    > Every publisher record must have a paper.

12. **Partial Participation**

    * ✅ `author_data` may exist without being in `paper_author` (i.e., unused authors exist).

13. **Foreign Key Constraint**

    * ✅ Present everywhere:
      `paper_author.paper_id` → `meta_data.paper_id`,
      `paper_author.author_id` → `author_data.author_id`, etc.

14. **Normalization to 3NF**

    * ✅ Avoided redundancy by separating `mainfilters`, `keywords`, `concepts`, etc.

    > Each value stored only once with lookup/join references.

15. **Reference Tables (Lookups)**

    * ✅ `domain_name`, `field_name`, `subfield_name`, `concept_name`, `topic_name`

    > Normalized entities with ID-name pairs.

16. **Multi-Entity Relationship**

    * ✅ `funder_table(paper_id, funder_id)`

    > Connects papers and funders.

17. **Participation Constraints Defined**

    * ✅ `paper_author`: Full participation from `author_data` to `meta_data`.
    * ✅ `funder_table`: Optional participation from both sides.

---


🧠 Outcomes and Learnings:
Gained hands-on experience in real-world ER modeling using an open, non-relational scholarly dataset.

Transformed semi-structured JSON into a well-structured relational schema.

Applied data modeling best practices, ensuring high data quality, integrity, and extensibility.

Prepared the foundation for advanced querying, analytics, and possible data warehousing.

