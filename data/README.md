# Dataset Information
This dataset(raw) is sourced from Kaggle and has been filtered to include only data after January 1, 2020, in order to reduce its volume.

# Description
The dataset consists of multiple CSV files containing structured information on: 
- Competitions 
- Games
- Clubs  
- Players
- Appearances 
    
Each file includes attributes describing the respective entities and IDs that allow for joining different files together for analysis.

# Data Source
This dataset originates from Kaggle, where it is automatically updated weekly. The original dataset includes longer historical data, but this sample focuses on post-2020 records to manage storage and processing efficiency.

### Sample data
The sample datasets, located within the 'sample' directory, are extracted from the raw datasets. Each sample dataset contains the first 100 records of its corresponding raw dataset. These samples were created for portability and accessibility.

### Others
Other sample datasets were generated during the pipeline's execution to showcase how the project was completed and fulfilled the project requirements.

### Contents of the directory

```
data
├── raw
│   ├── appearance.csv
│   ├── club_games.csv
│   ├── clubs.csv
│   ├── competitions.csv
│   ├── game_events.csv
│   ├── game_lineups.csv
│   ├── games.csv
│   ├── players.csv
│   ├── player_valuations.csv
│   └── transfers.csv
├── README.md
├── sample
│   ├── sample_appearance.csv
│   ├── sample_club_games.csv
│   ├── sample_clubs.csv
│   ├── sample_competitions.csv
│   ├── sample_game_events.csv
│   ├── sample_game_lineups.csv
│   ├── sample_games.csv
│   ├── sample_players.csv
│   ├── sample_player_valuations.csv
│   └── sample_transfers.csv
├── sample_bronze_layer_pipeline_stats.csv
├── sample_metadata.csv
└── sample_silver_layer_pipeline_stats.csv

```

