A Python desktop application utilizing Neo4j for database management and PyQt5 for an intuitive user interface. Search, analyze, and visualize research paper relationships effortlessly.


# Research Paper Citation and Classification

This project is a Python-based desktop application designed to search and analyze a research papers database stored in a Neo4j graph database. It allows users to perform queries such as checking if one paper cites another directly or indirectly, and displaying the full classification of a paper. The application provides a user-friendly interface to interact with the database and retrieve relevant information efficiently.

- **Research Paper Citation and Classification:** The core functionality of the project revolves around searching and analyzing research papers. This involves checking if one paper cites another directly or indirectly, as well as displaying the classification of a paper.
- **Neo4j:** Neo4j serves as the database management system for storing and querying research paper data. Its graph-based structure is well-suited for representing relationships between papers, such as citations and classifications.
- **PyQt5:** PyQt5 is used to develop the graphical user interface (GUI) for the application. It provides a set of Python bindings for the Qt framework, allowing for the creation of cross-platform desktop applications with rich UI features.


## Table of Contents

- [Features](#features)
- [Technologies Used](#technologies-used)
- [Installation](#installation)
- [Usage](#usage)
- [Contributing](#contributing)

## Features

- **Check if one paper cites another directly or indirectly.**
- **Display the full classification of a paper.**
- **User-friendly interface for easy interaction with the database.**
- **Efficient retrieval of relevant information from the research papers database.**
- **Support for direct and indirect citation path visualization.**
- **Environment variable-based configuration for enhanced security.**


## Technologies Used

- **Python**
- **PyQt5 (for GUI)**
- **Neo4j (as the graph database)**
- **python-dotenv (for managing environment variables)**


## Installation and Setup

1. **Clone the repository:**

   ```bash
      git clone https://github.com/onkaryemul/Research-Paper-Citation-and-Classification-using-Neo4j-and-PyQt5.git
   ```

2. **Navigate to the project directory:**

   ```bash
      cd Research-Paper-Citation-and-Classification-using-Neo4j-and-PyQt5
   ```
   
3. **Install the required dependencies:**
   
    ```bash
       pip install pyqt5 neo4j python-dotenv
    ```

4. **Instructions for moving csv files to the import directory within your Neo4j installation directory:**
   - Locate your Neo4j installation directory.
   - Inside the Neo4j installation directory, find the import folder.
   - Copy or move the cora_content.csv file from your downloads folder to the import folder.
     
   - **Make sure to move the `cora_content.csv` and `cora_cites.csv` files to the `import directory` within your `Neo4j installation directory`.**
   - **Additionally, ensure that Neo4j has read permissions for the file and that the file is correctly formatted for CSV import.**

5. **Set up the Neo4j database with the following commands:**
   - In Neo4j Browser, write and execute following Cypher queries to load the CSV file into the database.
   
   - **Make sure to adjust the file path in the LOAD CSV query to match the location of your CSV file within the Neo4j import directory.**
   
   - **Load data for research paper:**
   - a. **Load the nodes:**

      ```sql
         LOAD CSV WITH HEADERS FROM 'file:///cora_content.csv' AS line FIELDTERMINATOR ',' CREATE (:Paper {id: line.paper_id, class: line.label})
      ```
                   OR
      ```sql
         LOAD CSV WITH HEADERS FROM 'https://raw.githubusercontent.com/ngshya/datasets/master/cora/cora_content.csv' AS line FIELDTERMINATOR ',' CREATE (:Paper {id: line.paper_id, class: line.label})
      ```

   - b. **Load the relationships:**

      ```sql
         LOAD CSV WITH HEADERS FROM 'file:///cora_cites.csv' AS line FIELDTERMINATOR ','  MATCH (citing_paper:Paper {id: line.citing_paper_id}), (cited_paper:Paper {id: line.cited_paper_id}) CREATE (citing_paper)-[:CITES]->(cited_paper)
      ```
                  OR     
      ```sql
         LOAD CSV WITH HEADERS FROM 'https://raw.githubusercontent.com/ngshya/datasets/master/cora/cora_cites.csv' AS line FIELDTERMINATOR ',' MATCH (citing_paper:Paper {id: line.citing_paper_id}),(cited_paper:Paper {id: line.cited_paper_id}) CREATE (citing_paper)-[:CITES]->(cited_paper)
      ```

   - **These commands allow users to load CSV files into Neo4j using either a local file path (`file:///`) or a remote URL.**


## Usage

1. **.env Configuration:**
   **Create a .env file in the project root folder and set the following environment variables:**
      
    ```env
      DB_USERNAME=your_username
      DB_PASSWORD=your_password
      PORT=7687
    ```
    
    Replace `your_username` with your Neo4j database username, `your_password` with your database password, and 7687 with the port on which your Neo4j database has the Bolt protocol enabled.
    - **Additionally, make sure to specify the port on which Bolt is enabled for your Neo4j database.**
    - For assistance on finding the Bolt port, please refer to the Neo4j documentation or check your Neo4j configuration settings.
   
2. **Run the application:**

    ```bash
       python main.py
    ```

3. **Use the interface to perform queries on the research papers database.**


## Contributing

Contributions are welcome! Feel free to fork the repository, make improvements, and submit a pull request. Please follow best practices and maintain code clarity.

If you would like to contribute to the project, follow these steps:

1. Fork the repository.

2. Create a new branch:

   ```bash
     git checkout -b feature/your-feature-name
   ```
   
3. Make your changes and commit:

   ```bash
     git commit -m "Add your feature"
   ```

4. Push to your branch:

   ```bash
     git push origin feature/your-feature-name
   ```
   
5. Create a pull request on GitHub.
