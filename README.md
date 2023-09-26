# Healthcare Patient Data
The purpose of this project is to keep track of individual patient's data by asking ChatGPT questions about my patient's history. Additionally, I want to track any outbreaks by clustering the patients with similar symptoms.

I start this project by obtaining realistic synthetic patient data from Synthea. SyntheaTM is a Synthetic Patient Population Simulator. The output is synthetic, realistic (but not real), patient data and associated health records in a variety of formats.

Obtaining patient data from Synthea's Github repository
First, clone the Github repository. In the terminal, write: git clone https://github.com/synthetichealth/synthea.git
Navigate to the Synthea directory: cd synthea
Build Synthea ./gradlew build check test (~12 mins to build)
Run Synthea: ./run_synthea
For further customization, such as to get patient data from a specific state: ./run_synthea -p 10000 Tennessee "Nashville"
Successful build.
Now, I can find inside my synthea folder > output > FHIR > json files. Load the json data in here.
To modify synthea.properties file and export patients' symptoms:

Navigate to the src/main/resources directory within the Synthea directory.
Open the synthea.properties file.
Change exporter.symptoms.csv.export = true.
exporter.symptoms.mode = 0 to restrict the export to conditions occurred during the last {exporter.years_of_history} years, or set to any other value for the lifetime of the person.
Save and close the synthea.properties file.
Back in the terminal,./run_synthea -p 1000 Tennessee.
After Synthea completes the data generation, go to output/symptoms/csv within the Synthea directory.

