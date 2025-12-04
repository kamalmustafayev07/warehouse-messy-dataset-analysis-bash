# Warehouse Messy Dataset Analysis

## Overview
This repository contains Bash and AWK scripts for cleaning, analyzing, and visualizing a messy warehouse inventory dataset. The project demonstrates data preparation techniques, statistical computations, and generation of insights using lightweight, reproducible tools. For detailed analysis, including methods, findings, limitations, and conclusions, refer to the accompanying presentation PDF (`data-bash-project.pdf`).

## Dataset
The dataset is a CSV file (`warehouse_messy_data.csv`) sourced from GitHub: [https://github.com/eyowhite/Messy-dataset/blob/main/warehouse_messy_data.csv](https://github.com/eyowhite/Messy-dataset/blob/main/warehouse_messy_data.csv). It includes approximately 1000 entries across 10 columns: Product ID, Product Name, Category, Warehouse, Location, Quantity, Price, Supplier, Status, and Last Restocked.

## Requirements
- Bash shell
- AWK (standard on most Unix-like systems)
- GNUplot for generating visualizations
- No additional dependencies; scripts are designed for efficiency and portability.

## Usage
1. **Clone the Repository**:
   ```
   git clone <repository-url>
   cd warehouse-messy-dataset-analysis
   ```

2. **Data Cleaning**:
   Execute the cleaning scripts in sequence on `warehouse_messy_data.csv`. These handle whitespace trimming, duplicate checks, missing value imputation (e.g., means for numerical columns, latest date for dates), and type standardization.
   - Refer to the scripts in `SCRIPTS` for detailed commands, such as:
     ```
     awk -F',' '{for(i=1;i<=NF;i++) gsub(/^ +| +$/,"",$i) print}' OFS=',' warehouse_messy_data.csv > temp.csv && mv temp.csv warehouse_messy_data.csv
     ```
   - Impute missing quantities and prices with column means.
   - Replace textual values (e.g., "two hundred" to 200).
   - Fill missing dates with the most recent date in the column.

3. **Statistical Analysis**:
   Compute descriptive statistics, aggregations, correlations, and distributions.
   - Scripts are provided in `SCRIPTS` under "#SCRIPTS FOR STATISTICS".
   - Outputs are generated as CSV or TXT files (e.g., `quantity_price_stats.csv`, `correlation_qty_price.csv`).
   - Example: Count total records:
     ```
     awk 'NR>1 {count++} END {print count > "total_records.txt"}' warehouse_messy_data.csv
     ```

4. **Visualizations**:
   Use GNUplot to create plots from the aggregated data.
   - Scripts are in `SCRIPTS` under "#SCRIPTS FOR VISUALIZATION".
   - Generates PNG files (e.g., `category_quantity_price.png`).
   - Example for Total Quantity vs Total Price per Category:
     ```
     set datafile separator ","
     set terminal pngcairo size 900,600 enhanced
     set output "category_quantity_price.png"
     # Additional GNUplot commands as detailed in SCRIPTS
     ```

Run the scripts in order for a complete workflow. Ensure `warehouse_messy_data.csv` is present in the working directory.

## References
- [GNU AWK Manual](https://www.gnu.org/software/gawk/manual/)
- [Bash Scripting Tutorial for Beginners](https://linuxconfig.org/bash-scripting-tutorial-for-beginners)
- [AWK Examples](https://earthly.dev/blog/awk-examples/)
- [Stack Overflow: Redirect Command Output with AWK](https://stackoverflow.com/questions/8490500/redirect-command-output-with-awk)
- [GNUplot Data Tutorials](https://ctcms-uq.github.io/data_tutorials/gnuplot.html)
