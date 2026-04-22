# Digimon Data Processing Project

## Overview
This project focuses on extracting, processing, and storing data related to Digimon. The data will be extracted from JSON files, processed to ensure consistency and usability, and finally stored in a PostgreSQL database for further analysis and usage.

## Project Structure
```
.
├── digimon_data.ipynb       # Jupyter Notebook for data processing
├── data/                    # Directory containing raw data files
│   ├── raw/                 # Subdirectory with raw JSON files
│   │   ├── attributes.json  # Attributes data
│   │   ├── digimons.json    # Digimon data
│   │   ├── fields.json      # Fields data
│   │   ├── levels.json      # Levels data
│   │   ├── skills.json      # Skills data
│   │   └── types.json       # Types data
```

## Workflow
1. **Data Extraction**:
   - The raw data is stored in JSON files located in the `data/raw/` directory.
   - These files contain information about Digimon attributes, levels, skills, types, and more.

2. **Data Processing**:
   - The data will be processed using Python in the Jupyter Notebook `digimon_data.ipynb`.
   - Processing includes cleaning, transforming, and ensuring the data is ready for database insertion.

3. **Data Storage**:
   - The processed data will be stored in a PostgreSQL database.
   - PostgreSQL is chosen for its robustness and ability to handle structured data efficiently.

## Requirements
To run this project, you need the following:

- Python 3.8 or higher
- PostgreSQL database
- Required Python libraries (listed in `requirements.txt` if available)

## How to Run
1. Clone the repository:
   ```bash
   git clone <repository-url>
   ```

2. Navigate to the project directory:
   ```bash
   cd digimon-data-set
   ```

3. Install the required Python libraries:
   ```bash
   pip install -r requirements.txt
   ```

4. Open the Jupyter Notebook:
   ```bash
   jupyter notebook digimon_data.ipynb
   ```

5. Follow the steps in the notebook to process the data and insert it into the PostgreSQL database.

## Database Schema
The PostgreSQL database will include the following tables:

- **Digimons**: Stores information about each Digimon.
- **Attributes**: Stores attribute data.
- **Levels**: Stores level data.
- **Skills**: Stores skill data.
- **Types**: Stores type data.
- **Fields**: Stores field data.

## Future Enhancements
- Add data visualization for better insights.
- Automate the data extraction and processing pipeline.
- Integrate an API for real-time data access.

## License
This project is licensed under the MIT License. See the LICENSE file for details.