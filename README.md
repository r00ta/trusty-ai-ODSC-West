# trusty-ai-ODSC-West

This repository contains an end to end demonstration that has been presented at the ODSC West by me. 

This repository does not cointain the instructions to build the kogito application and the PMML+DMN models that have been used: if you are looking for this information, you can find all the detailed steps [here](https://github.com/r00ta/from-data-to-kogito-demo).

Note: at the time this presentation has been created (14th Oct 2021) the Counterfactual analysis was a preview feature. The current Kogito release is `1.11` and **it is planned** that the Counterfactual analysis feature will be available from `1.13`. This means that the images provided in the docker-compose were created by me compiling the sources from the `main` branch and it was not possible to use the official images released by Kogito.  

## Requirements
The following tools must be installed on the system:

Docker >= 20.10.3
Docker-compose >= 1.25.2

## Step 1 - start docker compose

After you have checked out this repository, run from your terminal 
 
```bash
docker-compose -f dev/docker-compose.yaml up
```

## Step 2 - Send a request to the kogito application!

Open `http://localhost:8080/q/swagger-ui` from your brower and send a POST request to the endpoint `/myMortgage` with the following body:

```json
{
  "Age": 20,
  "MonthlySalary": 2000,
  "TotalAsset": 50000,
  "TotalRequired": 100000,
  "NumberInstallments": 150
}
```

in the response, you can see that the mortgage request is rejected and the risk score is

```json
{
  ...
  "Risk Score": 43.4781123346508,
  "Mortgage Approval": false,
  ...
}
```

## Step 3 - Use the Trusy UI!

Open `http://localhost:1338` on your browser. The Trusty UI will provide the list of executions of your kogito application. In addition to that, for each execution it provides some information about the inputs and the outcomes of the model, the model that has been used and two explaination features: 

1) **LIME**: 
2) **Counterfactual analysis**: 


