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

![Screenshot from 2021-10-14 15-10-51](https://user-images.githubusercontent.com/18282531/137323888-0c50ff6e-5e56-45bc-a3b0-3ebf7b92aa3e.png)

## Step 3 - Use the Trusy UI!

Open `http://localhost:1338` on your browser. The Trusty UI will provide the list of executions of your kogito application. 

![Screenshot from 2021-10-14 15-11-35](https://user-images.githubusercontent.com/18282531/137323965-731faf0a-657b-4899-b7e4-1c60c9f0da2a.png)

In addition to that, for each execution it provides some information about the inputs and the outcomes of the model

![Screenshot from 2021-10-14 15-12-05](https://user-images.githubusercontent.com/18282531/137324052-198d5607-5193-4407-8bb8-77eabac651a1.png)
![Screenshot from 2021-10-14 15-12-12](https://user-images.githubusercontent.com/18282531/137324059-9013e127-f913-4429-be43-5b63de55e4d7.png)

the model that has been used 

![Screenshot from 2021-10-14 15-12-37](https://user-images.githubusercontent.com/18282531/137324141-4d1b5e0f-20df-4e72-adea-cecf4d56e7f7.png)

and two explaination features: 

1) **LIME**: 
![Screenshot from 2021-10-14 15-13-14](https://user-images.githubusercontent.com/18282531/137324256-e39fc270-db5f-41da-8e7d-952717215043.png)

2) **Counterfactual analysis**: 
![Screenshot from 2021-10-14 15-13-38](https://user-images.githubusercontent.com/18282531/137324326-04770b5f-ab1a-4781-89f9-6d53430b8eb4.png)


