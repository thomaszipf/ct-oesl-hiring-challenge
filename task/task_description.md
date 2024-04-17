# Requirements for Data Engineering Challenge

## Task Description

The overall target of the task is:
1. Extraction of timeseries data for actual temperature (TEMPERATUR INNEN_IST) and pressure (DRUCK INNEN_IST) values per cycle, based on the overall timeseries data within the give timeframe (2024-04-08 00:00:00 until 2024-04-10 23:59:59).
2. Plot a set of temperature / pressure curves (line plot per cycle).
3. Describe your data transformation steps in a small document (can be PowerPoint Presentation or Markdown File).
4. BONUS (optional): Detect cycles that are not okay based on the average shape of the actual temperature (TEMPERATUR INNEN_IST) and pressure (DRUCK INNEN_IST) values per cycle.


### Parquet Files Structure

Given are multiple parquet files that contains timeseries data as an input.

#### Folder Structure

The input data is currently located within multiple parquet files (structured by date and time YYYY/MM/DD/HH).

```
data
├── config (tag definition)
├── machine_data (process values)
|   ├── 2022 (years)
|   |   ├── 11 (months)
|   |   |   ├── 17 (days)
|   |   |   |   ├── 15 (hours)
│   |   |   |   |   ├── uuid.parquet (parquet files grouped by tags)
```

#### Dataset Description

The following columns are available within the dataset:

| column          | datatype  | description                                                                                                                                                |
| --------------- | --------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------- |
| datapoint_uuid  | uuid      | The uuid of the datapoint describes the datapoint itself.                                                                                                  |
| hour            | string    | The hour column contains the hour as a string once the data was collected. Format is: YYYYMMDDHH                                                           |
| systime         | timestamp | The systime column contains a normalized timestamp in UTC time that shall be used as time column as per standard                                           |
| plctime         | timestamp | The plctime column contains a non normalized timestamp in local time. This timestamp shall not be used as default. Use of the systime column is mandatory! |
| sequence_number | integer   | The sequence_number is a number that will be increased until integer max. In many cases this column is not used and can be dropped                         |
| value_bool      | boolean   | The value of the datapoint that is of type boolean.                                                                                                        |
| value_bytes     | byte      | The value of the datapoint that is of type bytes.                                                                                                          |
| value_double    | float     | The value of the datapoint that is of type double or float.                                                                                                |
| value_integer   | integer   | The value of the datapoint that is of type integer.                                                                                                        |
| value_string    | string    | The value of the datapoint that is of type string.                                                                                                         |


#### Datapoint File Description

The second input is a json file, named [datapoints.json](../data/config/datapoints.json), that describes the collected datapoints. Those datapoints have an uuid and a defined datatype. According to the datatype the value is stored within one of the given value columns within the parquet files.

**Hint:** The following uuids are available within the dataset: 

```python
uuids = [
"feec5c34-e1ad-4090-94aa-75d7837b7695",
"f535808d-cc8b-47fc-9080-77fda2f37c42",
"9e25a283-a372-43b5-bd13-a4c2f7ece605",
"41590dca-3163-49b6-b02a-af31acbb0fd7",
"b5e027a1-da7c-4a30-99f0-0ce9203ede10",
"bf1135df-a008-4870-a735-708c928c1fea",
"ce969e1f-41d3-493e-9809-dde68cd520f0",
"5cde150d-c044-4e55-8c48-73321e0c0f27",
"67da707a-735b-497d-9870-40349919814c",
"00f9c223-6fd4-45ec-8ee2-62b9458c98fc",
"9d7f979a-c50e-494c-9ee0-082eabe3143f",
"8a1c7509-3c14-4f8f-b81c-0d44190ea305",
"52ba9c7e-0660-43a3-a33d-6de86ddf7f85",
"7826d0d5-73c5-47a3-ae05-9bef58b32693"
]
```

## General Programming Requirements

The following requirements need to be met and followed during the development phase:

1. Write Readable Code: Use clear variable names and keep functions focused on a single task.
2. Follow PEP 8: Adhere to the Python Enhancement Proposal 8 (PEP 8) style guide for Python code for consistency.
3. Use Functions and Modules: Break code into reusable functions and modules for better organization and reusability.
4. Handle Exceptions: Use try-except blocks to catch and manage exceptions, ensuring your program's robustness.
5. Leverage Built-ins and Libraries: Make use of Python’s built-in functions and external libraries to avoid reinventing the wheel.
6. Optimize Performance: Profile and optimize your code, focusing on bottlenecks, especially in loops and data processing.
7. Write Tests (optional): Implement unit tests to verify functionality and facilitate safe refactoring.
8. Document Your Code: Comment your code and use docstrings to explain function purposes and parameters.
9. Use Version Control: Manage your code with a version control system (like Git) to track changes and collaborate.
10. Follow the Zen of Python: Keep the Zen of Python (PEP 20) in mind as a guiding philosophy for Pythonic code design and development practices.

Happy Coding!