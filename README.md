###This is a react web applicaiton with simple modules

## How to Run this app:


### 1. docker build -t (image-name) .

### 2. Fill kubernetes/values.yaml file with your desired values like app name and port

### 3. helm install react-app ./kubernetes -n react-app --create-namespace

### 4. Now everything is ready to access your app on the selected port
