# Introduction
Performance test scripts

# Getting Started
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