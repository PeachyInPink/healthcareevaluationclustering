# Healthcare Patient Data
The purpose of this project is to keep track of individual patient's data by asking ChatGPT questions about my patient's history. Additionally, I want to track any outbreaks by clustering the patients with similar symptoms.

I start this project by obtaining realistic synthetic patient data from Synthea. SyntheaTM is a Synthetic Patient Population Simulator. The output is synthetic, realistic (but not real), patient data and associated health records in a variety of formats.

**Obtaining patient data from Synthea's Github repository**

1. First, clone the Github repository. In the terminal, write:

`git clone https://github.com/synthetichealth/synthea.git`

2. Navigate to the Synthea directory: 

`cd synthea`
3. Build Synthea

`./gradlew build check test` (~12 mins to build)

4. Run Synthea:

`./run_synthea`

5. For further customization, such as to get patient data from a specific state:

`./run_synthea -p 10000 Tennessee "Nashville"`

6. Successful build.

7. Now, I can find inside my synthea folder > output > FHIR > json files. Load the json data in here. 

To modify synthea.properties file and export patients' symptoms:

1. Navigate to the `src/main/resources` directory within the Synthea directory.

2. Open the `synthea.properties` file.

3. Change `exporter.symptoms.csv.export = true`.

4. `exporter.symptoms.mode = 0` to restrict the export to conditions occurred during the last {exporter.years_of_history} years, or set to any other value for the lifetime of the person.

5. Save and close the synthea.properties file.

6. Back in the terminal,`./run_synthea -p 1000 Tennessee`.

7. After Synthea completes the data generation, go to `output/symptoms/csv` within the Synthea directory.


**Executive Summary**

* Queried synthetic patient data from Synthea™, a Synthetic Patient Population Simulator, to generate realistic (artificial), patient data and associated health records for patients in the state of Tennessee.

* Performed data cleaning to extract practical symptom descriptions, eliminating non-alphabetic characters and extraneous whitespace from the symptom list, ensuring consistency for further analysis.

* Used the Jaccard Similarity Coefficient to measure the similarity between sets of symptoms, facilitating clustering analysis given the set-based nature of the symptom data.

* Performed Hierarchical Clustering with AgglomerativeClustering algorithm to cluster patients based on symptom similarities, which should help with outbreak tracking and patient categorization.

* Derived 40 distinct clusters of symptoms to efficiently categorize patients, setting a tracking protocol for potential outbreaks and understanding patient symptoms.

* Integrated a question-answering system with ChatGPT 3.5 to keep a dynamic record of individual patient's history, providing a seamless interface for querying patient data and gaining insights into their health conditions (no UI).

* Integrated a user-friendly website interface (UI) using Streamlit, enabling users to upload their CSV files containing hashed patient data. This portal integrates with the ChatGPT language model, facilitating immediate responses to healthcare workers inquiries regarding patient information.
