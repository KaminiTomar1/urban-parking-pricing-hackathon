# Urban Parking Pricing Hackathon

## Project Overview
This project develops a dynamic pricing system for urban parking lots, optimizing prices based on real-time data such as occupancy, queue length, traffic conditions, and competitor prices. The system uses three pricing models: a linear model based on occupancy, a demand-based model incorporating multiple factors, and a competitive model with rerouting suggestions. The solution leverages the `pathwaycom/pathway` library for streaming data processing and is implemented in a Google Colab notebook for the hackathon submission.

## Tech Stack
- **Programming Language**: Python 3.11
- **Libraries**:
  - `pathway` (v0.14.3): For streaming data processing and pipeline execution.
  - `pandas`: For data preprocessing and CSV handling.
  - `numpy`: For numerical computations and simulations.
  - `bokeh`: For interactive visualizations of price trends and occupancy.
- **Environment**: Google Colab for development and execution.
- **Dataset**: `dataset (1).csv` (provided by the hackathon, stored in `data/` folder).
- **Version Control**: GitHub for hosting the repository.

## Architecture Diagram
Below is the architecture diagram of the dynamic pricing system, created using Mermaid:

```mermaid
graph TD
    A[Input: dataset (1).csv] --> B[Preprocessing]
    B -->|Pandas| C[preprocessed_data.csv]
    C --> D[Pathway Streaming Pipeline]
    D -->|Load Data| E[Pathway Table]
    E -->|Apply Pricing Models| F[Model 1: Linear]
    E -->|Apply Pricing Models| G[Model 2: Demand-Based]
    E -->|Apply Pricing Models| H[Model 3: Competitive]
    F --> I[Output Table]
    G --> I
    H --> I
    I -->|Write CSV| J[output_prices.csv]
    J --> K[Visualization with Bokeh]
    K --> L[Price Trends Plot]
    K --> M[Occupancy & Queue Plot]
    J --> N[Report]

Project Architecture and Workflow
The project follows a structured pipeline to process parking data and generate dynamic prices:

Data Ingestion:
The input dataset (dataset (1).csv) contains parking lot data, including SystemCodeNumber, Occupancy, Capacity, QueueLength, TrafficConditionNearby, IsSpecialDay, VehicleType, Latitude, Longitude, LastUpdatedDate, and LastUpdatedTime.
Loaded using pandas in Google Colab.
Preprocessing:
Combine LastUpdatedDate and LastUpdatedTime into a timestamp column (ISO 8601 format).
Rename columns (e.g., SystemCodeNumber to parking_lot_id) for consistency.
Encode TrafficConditionNearby as numerical values (low=0, average=1, high=2).
Assign vehicle type weights (cycle=0.5, bike=0.75, car=1.0, truck=1.5).
Simulate competitor prices ($8–$12) due to missing data.
Save preprocessed data to preprocessed_data.csv.
Streaming Pipeline:
Use pathway (v0.14.3) to read preprocessed_data.csv as a streaming table with a defined schema (ParkingSchema).
Apply three pricing models:
Model 1 (Linear): Price = 10 + 0.5 * (Occupancy/Capacity).
Model 2 (Demand-Based): Price based on occupancy, queue, traffic, special day, and vehicle type, normalized and scaled.
Model 3 (Competitive): Adjusts price based on demand and competitor prices, with rerouting if occupancy > 90% and competitors are cheaper.
Compute distances between parking lots using the Haversine formula for rerouting logic.
Write results to output_prices.csv.
Visualization:
Load output_prices.csv with pandas.
Use bokeh to create interactive plots for price trends (Models 1–3) and occupancy/queue for lot BHMBCCMKT01.
Reporting:
A report is included in the notebook (dynamic_pricing_final.ipynb) summarizing the demand functions, assumptions, price changes, and visualizations.
How to Run
Open dynamic_pricing_final.ipynb in Google Colab.
Upload data/dataset (1).csv to Colab’s file system.
Run all cells to:
Install dependencies (pathway==0.14.3, pandas, numpy, bokeh).
Preprocess the dataset.
Execute the Pathway streaming pipeline.
Generate output_prices.csv.
Create visualizations and display the report.
Check console logs for debugging output (e.g., pipeline row processing).
Repository Structure
src/dynamic_pricing_final.ipynb: Main Colab notebook with the complete code.
data/dataset (1).csv: Input dataset.
README.md: This documentation file.
Notes
Ensure dataset (1).csv is in the data/ folder or adjust the file path in the notebook.
The code includes error handling for missing files, empty outputs, and timestamp parsing issues.
The report is embedded in the notebook but can be exported as a PDF if needed (use Colab’s File > Print > Save as PDF).
License
MIT License

Commit the Changes:

Scroll to the bottom of the edit page.
In the “Commit changes” section:
Add a commit message like “Update README with project details and architecture”.
Select Commit directly to the main branch.
Click Commit changes.
Verify the README:

Refresh your repository page (https://github.com/KaminiTomar1/urban-parking-pricing-hackathon).
The README.md should now display with formatted text, a Mermaid diagram (rendered as a flowchart), and all sections.
Check that the diagram renders correctly (GitHub supports Mermaid natively).
Optional: Adjust for Repository Structure:

If you organized files into src/ and data/ folders (as suggested in the previous step), the README.md above already reflects this (src/dynamic_pricing_final.ipynb and data/dataset (1).csv).
If you uploaded files directly to the root directory (not in folders), update the “Repository Structure” section in the README.md to:
markdown



## Repository Structure
- `dynamic_pricing_final.ipynb`: Main Colab notebook with the complete code.
- `dataset (1).csv`: Input dataset.
- `README.md`: This documentation file.
Edit README.md again (click the pencil icon), update the section, and commit with a message like “Update README for root directory structure”.
