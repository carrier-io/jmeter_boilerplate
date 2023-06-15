# Introduction
This repository contains the following components:

- JMeter Test Scripts: ready to use examples for creating performance test scripts tailored to your application's needs.
- Starting Azure Pipeline: A sample pipeline configuration file that demonstrates how to integrate performance testing Azure Pipelines. 

# Getting Started
> To integrate in Azure DevOps
1. Sign in to your Azure DevOps account.
2. Go to the Azure DevOps project where you want to add the GitHub integration.
3. Navigate to the Pipelines section.
4. Click on the "New Pipeline" button to create a new pipeline.
5. Choose the appropriate source control system, it our case it is GitHub.
6. Select the repository where your `azure-pipeline.yml` file is located
7. Azure DevOps will detect the `azure-pipeline.yml` file in your repository. Click on it to proceed.
8. Choose the pipeline configuration that matches your needs, such as YAML.
9. Review the pipeline configuration in the YAML editor. If necessary, make any modifications to suit your requirements.
10. In the YAML file, locate the "Parameters" section. This is where you can define and set the variables used in the pipeline.
11. Modify `$(PoolName)`, `$(MySecretToken)` and other values as needed, or you can reference variables or pipeline variables using the `$(VariableName)` syntax.

```yaml
variables:
  - name: TEST
    value: 'mixed'
  - name: ENV_URL
    value: 'pythonanywhere.com'
  - name: VUSERS
    value: 10
  - name: DURATION
    value: 300
  - name: RAMP_UP
    value: 30
  - name: THINK_TIME
    value: 5000
  - name: THINK_TIME_DEVIATION
    value: 5000
  - name: generateReport
    value: true
  - name: poolName
    value: $(PoolName)
  - name: token
    value: $(MySecretToken)
```

11. Save the changes to the `azure-pipeline.yml` file.
12. Proceed with configuring the pipeline settings, such as agent pool, triggers, and stages, according to your requirements.
13. Click on the "Save and Run" button to save the pipeline configuration and trigger a pipeline run.

That's it! Your GitHub repository is now integrated with the existing default pipeline in Azure DevOps, and the specified variables are set for the pipeline runs.

> To run tests locally
1. Install Java 1.8+ version
2. Download [JMeter](https://dlcdn.apache.org//jmeter/binaries/apache-jmeter-5.5.zip)
3. Unzip
4. Add JMeter "bin" folder to PATH environment var
5. Open test in UI
```bash
$ jmeter -t tests/mixed.jmx
```

# Test Locally
1. Add JMeter "bin" folder to PATH environment var
2. Run in Non-Gui:
```bash
jmeter -n -t tests/{test_name}.jmx -l result.jtl -e -o html_report -DENV_URL={ENV} -DVUSERS={VUSERS} -DDURATION={DURATION} -DRAMP_UP={RAMP_UP} -Jjmeter.reportgenerator.overall_granularity=1000
```
where
```bash 
test_name:                # Sentara_Mixed(all tests), Scn01_Find_Doc,Scn02_Find_Loc,Scn03_Billing,Scn04_My_Chart,Scn05_Careers
ENV                       # sentaracom-prod.sentara.com domain against which to run test 
VUSERS                    # Number of virtual users/threads
DURATION                  # Test duration
RAMP_UP                   # Time until which all vUsers will be active in the system
jmeter.reportgenerator.overall_granularity=1000      # Data points granularity
```

3. Open report
```bash 
open html_report/index.html 
```