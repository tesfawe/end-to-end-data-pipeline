# Data Contract for Football Dataset Pipeline

## 1. Title
**Title**: Data Contract (Football Dataset Pipeline)

## 2. Dataset Overview
- **Source**: Kaggle (Fetched Weekly)
- **ETL Pipeline Owner**: Tesfay Tesfay
- **Storage Layers**: Bronze → Silver → Gold
- **Use Case**: Football analytics, player statistics, game events.

## 3. Schema Definitions

---
### appearance

| Column Name                   | Type    | Nullable | Constraints                                      |
|-------------------------------|---------|----------|-------------------------------------------------|
| `appearance_id`               | String  | Yes      | Unique identifier for each appearance.          |
| `game_id`                     | Integer | Yes      | References a game in `games`.                   |
| `player_id`                   | Integer | Yes      | References a player in `players`.               |
| `player_club_id`              | Integer | Yes      | References a club in `clubs`.                   |
| `player_current_club_id`      | Integer | Yes      | References a club in `clubs`.                   |
| `date`                        | Date    | Yes      | Must be a valid date.                           |
| `player_name`                 | String  | Yes      |                                                 |
| `competition_id`              | String  | Yes      | References a competition in `competitions`.     |
| `yellow_cards`                | Integer | Yes      |                                                 |
| `red_cards`                   | Integer | Yes      |                                                 |
| `goals`                       | Integer | Yes      |                                                 |
| `assists`                     | Integer | Yes      |                                                 |
| `minutes_played`              | Integer | Yes      |                                                 |

#### Data Quality Rules
- **Primary Key Uniqueness**:
  - `appearance_id` must be unique.
- **Referential Integrity**:
  - `game_id` must exist in `games`.
  - `player_id` must exist in `players`.
  - `player_club_id` and `player_current_club_id` must exist in `clubs`.
  - `competition_id` must exist in `competitions`.
- **Value Constraints**:
  - `yellow_cards`, `red_cards`, `goals`, `assists`, `minutes_played` must be non-negative integers.
  - `date` must follow ISO 8601 format (`YYYY-MM-DD`).

---

### game_events

| Column Name           | Type    | Nullable | Constraints                                      |
|-----------------------|---------|----------|-------------------------------------------------|
| `game_event_id`       | String  | Yes      | Unique identifier for each game event.          |
| `date`                | Date    | Yes      | Must be a valid date.                           |
| `game_id`             | Integer | Yes      | References a game in `games`.                   |
| `minute`              | Integer | Yes      |                                                 |
| `type`                | String  | Yes      |                                                 |
| `club_id`             | Integer | Yes      | References a club in `clubs`.                   |
| `player_id`           | Integer | Yes      | References a player in `players`.               |
| `description`         | String  | Yes      |                                                 |

#### Data Quality Rules
- **Primary Key Uniqueness**:
  - `game_event_id` must be unique.
- **Referential Integrity**:
  - `game_id` must exist in `games`.
  - `club_id` must exist in `clubs`.
  - `player_id` must exist in `players`.
- **Value Constraints**:
  - `minute` must be a non-negative integer.
  - `date` must follow ISO 8601 format (`YYYY-MM-DD`).

---

### club_games

| Column Name                | Type    | Nullable | Constraints                                      |
|----------------------------|---------|----------|-------------------------------------------------|
| `game_id`                  | Integer | Yes      | References a game in `games`.                   |
| `club_id`                  | Integer | Yes      | References a club in `clubs`.                   |
| `own_goals`                | Integer | Yes      |                                                 |
| `own_position`             | Integer | Yes      |                                                 |
| `own_manager_name`         | String  | Yes      |                                                 |
| `opponent_id`              | Integer | Yes      | References a club in `clubs`.                   |
| `opponent_goals`           | Integer | Yes      |                                                 |
| `opponent_position`        | Integer | Yes      |                                                 |
| `opponent_manager_name`    | String  | Yes      |                                                 |
| `hosting`                  | String  | Yes      |                                                 |
| `is_win`                   | Boolean | Yes      |                                                 |

#### Data Quality Rules
- **Referential Integrity**:
  - `game_id` must exist in `games`.
  - `club_id` and `opponent_id` must exist in `clubs`.
- **Value Constraints**:
  - `own_goals`, `own_position`, `opponent_goals`, `opponent_position` must be non-negative integers.
  - `is_win` must be a boolean (`true`/`false`).

---

## clubs

| Column Name                   | Type    | Nullable | Constraints                                      |
|-------------------------------|---------|----------|-------------------------------------------------|
| `club_id`                     | Integer | Yes      | Unique identifier for each club.                |
| `club_code`                   | String  | Yes      |                                                 |
| `name`                        | String  | Yes      |                                                 |
| `domestic_competition_id`     | Integer | Yes      | References a competition in `competitions`.     |
| `squad_size`                  | Integer | Yes      |                                                 |
| `average_age`                 | Double  | Yes      |                                                 |
| `foreigners_number`           | Integer | Yes      |                                                 |
| `foreigners_percentage`       | Double  | Yes      |                                                 |
| `national_team_players`       | Integer | Yes      |                                                 |
| `stadium_name`                | String  | Yes      |                                                 |
| `stadium_seats`               | Integer | Yes      |                                                 |
| `net_transfer_record`         | String  | Yes      |                                                 |
| `last_season`                 | Integer | Yes      |                                                 |
| `filename`                    | String  | Yes      |                                                 |
| `url`                         | String  | Yes      |                                                 |

#### Data Quality Rules
- **Primary Key Uniqueness**:
  - `club_id` must be unique.
- **Referential Integrity**:
  - `domestic_competition_id` must exist in `competitions`.
- **Value Constraints**:
  - `squad_size`, `foreigners_number`, `national_team_players`, `stadium_seats`, `last_season` must be non-negative integers.
  - `average_age` must be a positive number.
  - `foreigners_percentage` must be between `0` and `100`.

---

### competitions

| Column Name                       | Type    | Nullable | Constraints                                      |
|-----------------------------------|---------|----------|-------------------------------------------------|
| `competition_id`                 | String  | Yes      | Unique identifier for each competition.         |
| `competition_code`               | String  | Yes      |                                                 |
| `name`                           | String  | Yes      |                                                 |
| `sub_type`                       | String  | Yes      |                                                 |
| `type`                           | String  | Yes      |                                                 |
| `country_id`                     | Integer | Yes      |             |
| `country_name`                   | String  | Yes      |                                                 |
| `domestic_league_code`           | String  | Yes      |                                                 |
| `confederation`                  | String  | Yes      |                                                 |
| `is_major_national_league`       | Boolean | Yes      |                                                 |

#### Data Quality Rules
- **Primary Key Uniqueness**:
  - `competition_id` must be unique.
- **Value Constraints**:
  - `is_major_national_league` must be a boolean (`true`/`false`).

---

### game_lineups

| Column Name           | Type    | Nullable | Constraints                                      |
|-----------------------|---------|----------|-------------------------------------------------|
| `date`                | String  | Yes      |                                                 |
| `game_id`             | Integer | Yes      | References a game in `games`.                   |
| `player_id`           | Integer | Yes      | References a player in `players`.               |
| `club_id`             | Integer | Yes      | References a club in `clubs`.                   |
| `player_name`         | String  | Yes      |                                                 |
| `type`                | String  | Yes      |                                                 |
| `position`            | String  | Yes      |                                                 |
| `number`              | Integer | Yes      |                                                 |

#### Data Quality Rules
- **Referential Integrity**:
  - `game_id` must exist in `games`.
  - `player_id` must exist in `players`.
  - `club_id` must exist in `clubs`.
- **Value Constraints**:
  - `number` must be a non-negative integer.
  - `date` must follow ISO 8601 format (`YYYY-MM-DD`).

---

### games

| Column Name                       | Type    | Nullable | Constraints                                      |
|-----------------------------------|---------|----------|-------------------------------------------------|
| `game_id`                         | Integer | Yes      | Unique identifier for each game.                |
| `competition_id`                  | String  | Yes      | References a competition in `competitions`.     |
| `season`                          | Integer | Yes      |                                                 |
| `round`                           | String  | Yes      |                                                 |
| `date`                            | Date    | Yes      | Must be a valid date.                           |
| `home_club_id`                    | Integer | Yes      | References a club in `clubs`.                   |
| `away_club_id`                    | Integer | Yes      | References a club in `clubs`.                   |
| `home_club_goals`                 | Integer | Yes      |                                                 |
| `away_club_goals`                 | Integer | Yes      |                                                 |
| `home_club_position`              | Float   | Yes      |                                                 |
| `away_club_position`              | Float   | Yes      |                                                 |
| `home_club_manager_name`          | String  | Yes      |                                                 |
| `away_club_manager_name`          | String  | Yes      |                                                 |
| `stadium`                         | String  | Yes      |                                                 |
| `attendance`                      | Integer | Yes      |                                                 |
| `referee`                         | String  | Yes      |                                                 |
| `home_club_formation`            | String  | Yes      |                                                 |
| `away_club_formation`            | String  | Yes      |                                                 |
| `home_club_name`                 | String  | Yes      |                                                 |
| `away_club_name`                 | String  | Yes      |                                                 |
| `competition_type`               | String  | Yes      |                                                 |

#### Data Quality Rules
- **Primary Key Uniqueness**:
  - `game_id` must be unique.
- **Referential Integrity**:
  - `competition_id` must exist in `competitions`.
  - `home_club_id` and `away_club_id` must exist in `clubs`.
- **Value Constraints**:
  - `season`, `home_club_goals`, `away_club_goals`, `attendance` must be non-negative integers.
  - `home_club_position`, `away_club_position` must be non-negative floats.
  - `date` must follow ISO 8601 format (`YYYY-MM-DD`).

---

### player_valuations

| Column Name                               | Type    | Nullable | Constraints                                      |
|-------------------------------------------|---------|----------|-------------------------------------------------|
| `player_id`                               | Integer | Yes      | References a player in `players`.               |
| `date`                                    | Date    | Yes      | Must be a valid date.                           |
| `market_value_in_eur`                     | Float   | Yes      |                                                 |
| `current_club_id`                         | Integer | Yes      | References a club in `clubs`.                   |
| `player_club_domestic_competition_id`     | String  | Yes      | References a competition in `competitions`.     |

#### Data Quality Rules
- **Referential Integrity**:
  - `player_id` must exist in `players`.
  - `current_club_id` must exist in `clubs`.
  - `player_club_domestic_competition_id` must exist in `competitions`.
- **Value Constraints**:
  - `market_value_in_eur` must be a non-negative float.
  - `date` must follow ISO 8601 format (`YYYY-MM-DD`).

---

### players

| Column Name                               | Type    | Nullable | Constraints                                      |
|-------------------------------------------|---------|----------|-------------------------------------------------|
| `player_id`                               | Integer | Yes      | Unique identifier for each player.              |
| `first_name`                              | String  | Yes      |                                                 |
| `last_name`                               | String  | Yes      |                                                 |
| `last_season`                             | Date    | Yes      | Must be a valid date.                           |
| `current_club_id`                         | Integer | Yes      | References a club in `clubs`.                   |
| `player_code`                             | String  | Yes      |                                                 |
| `country_of_birth`                        | String  | Yes      |                                                 |
| `city_of_birth`                           | String  | Yes      |                                                 |
| `country_of_citizenship`                  | String  | Yes      |                                                 |
| `date_of_birth`                           | Date    | Yes      | Must be a valid date.                           |
| `sub_position`                            | String  | Yes      |                                                 |
| `position`                                | String  | Yes      |                                                 |
| `foot`                                    | String  | Yes      |                                                 |
| `height_in_cm`                            | Double  | Yes      |                                                 |
| `contract_expiration_date`                | Date    | Yes      | Must be a valid date.                           |
| `agent_name`                              | String  | Yes      |                                                 |
| `current_club_domestic_competition_id`    | String  | Yes      | References a competition in `competitions`.     |
| `current_club_name`                       | String  | Yes      |                                                 |
| `market_value_in_eur`                     | Float   | Yes      |                                                 |
| `highest_market_value_in_eur`             | Float   | Yes      |                                                 |

#### Data Quality Rules
- **Primary Key Uniqueness**:
  - `player_id` must be unique.
- **Referential Integrity**:
  - `current_club_id` must exist in `clubs`.
  - `current_club_domestic_competition_id` must exist in `competitions`.
- **Value Constraints**:
  - `height_in_cm` must be a positive number.
  - `market_value_in_eur`, `highest_market_value_in_eur` must be non-negative floats.
  - `last_season`, `date_of_birth`, `contract_expiration_date` must follow ISO 8601 format (`YYYY-MM-DD`).

---

### transfers

| Column Name               | Type    | Nullable | Constraints                                      |
|---------------------------|---------|----------|-------------------------------------------------|
| `player_id`               | Integer | Yes      | References a player in `players`.               |
| `transfer_date`           | Date    | Yes      | Must be a valid date.                           |
| `transfer_season`         | String  | Yes      |                                                 |
| `from_club_id`            | Integer | Yes      | References a club in `clubs`.                   |
| `to_club_id`              | Integer | Yes      | References a club in `clubs`.                   |
| `from_club_name`          | String  | Yes      |                                                 |
| `to_club_name`            | String  | Yes      |                                                 |
| `market_value_in_eur`     | Double  | Yes      |                                                 |
| `player_name`             | String  | Yes      |                                                 |

#### Data Quality Rules
- **Referential Integrity**:
  - `player_id` must exist in `players`.
  - `from_club_id` and `to_club_id` must exist in `clubs`.
- **Value Constraints**:
  - `market_value_in_eur` must be a non-negative double.
  - `transfer_date` must follow ISO 8601 format (`YYYY-MM-DD`).
## 5. Update & Refresh Policy
- **Data Refresh Frequency**: Weekly (on Sundays).
- **ETL Processing Time**: Between 02:00 - 03:00 North Europe Time Zone.
- **Full Data Replacement**: The entire dataset is replaced with the latest data from the source during each refresh.
- **Schema Enforcement**: Schema validation is performed during the update process to ensure compatibility with downstream systems. 

## 6. Ownership & Responsibilities
- **Pipeline Owner**: Tesfay Tesfay
- **Monitoring & Alerts**: Schema drift alerts via Databricks Unity Catalog and Delta Live Tables.

## 7. Handling Breaking Changes
- **Schema Changes**: New columns must be backward-compatible.
- **Deprecation Notice**: Any schema changes require a month advance notice.



