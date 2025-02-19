# AWS Practise Project

This project has been overwritten with the contents of [DJH23/aws-practise](https://github.com/DJH23/aws-practise).

Steps:

1. Clone the repository:
   ```bash
   git clone https://github.com/DJH23/aws-practise.git
   cd aws-practise
   npm install
   ```
2. For AWS Amplify Gen 2 and Vue3 integration:
 - Configure AWS Amplify:
    - From the Amplify Console, go to your app > Backend environments > Deployed backend resources
    - Copy the configuration details or use the AWS CLI command:
      ```bash
    amplify pull --appId d2rdh0vzjxobb5 --envName dev
      ```
    - This will automatically set up your local configuration
3. Run the local dev server:
   ```bash
   npm run dev
   ```
4. Commit and push changes to update the deployed app.
