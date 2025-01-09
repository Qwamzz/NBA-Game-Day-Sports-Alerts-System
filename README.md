# **NBA Game Day Notifications: Real-Time Alerts System**

## **Overview**
This project is designed to keep NBA fans updated with live game scores through automated notifications delivered via SMS or email. The system integrates **AWS cloud services** such as Lambda, SNS, and EventBridge with the **NBA Game API** to fetch and distribute game data efficiently. This solution demonstrates the application of serverless architectures for real-world use cases, highlighting the capabilities of AWS for building scalable and secure systems.

---

## **Features**
1. **Live Score Updates**: Fetches real-time NBA scores using the external NBA Game API.
2. **Automated Notifications**: Sends formatted updates via Amazon Simple Notification Service (SNS) to subscribed users.
3. **Scheduled Execution**: Uses Amazon EventBridge to schedule periodic score updates automatically.
4. **Secure Design**: Implements IAM roles and policies to ensure the system adheres to the principle of least privilege.
5. **Customizable Notifications**: Supports multiple subscription types, including email and SMS, allowing users to choose their preferred notification method.

---

## **Technical Architecture**
The solution is structured to maximize scalability and reliability:

1. **NBA API**: Fetches real-time game scores.
2. **AWS Lambda**: Processes game data and formats notifications.
3. **Amazon SNS**: Distributes notifications to users via email and SMS.
4. **Amazon EventBridge**: Automates Lambda function triggers based on a set schedule.
5. **IAM Roles**: Enforces least-privilege access to ensure system security.

### Architecture Diagram
![diagram-export-09-01-2025-11_50_58](https://github.com/user-attachments/assets/1d521116-4961-4916-ab2d-670d2589007f)


## **Technologies Used**
- **Programming Language**: Python 3.x
- **Cloud Provider**: AWS
- **Core Services**: 
  - **AWS Lambda**: For serverless function execution.
  - **Amazon SNS**: For notification distribution.
  - **Amazon EventBridge**: For scheduling and automation.
- **External API**: NBA Game API (provided by SportsData.io).
- **Security**: IAM roles and policies tailored for specific services.

---

## **Project Structure**
```
game-day-notifications/
├── src/
│   ├── gd_notifications.py          # Main Lambda function script
├── policies/
│   ├── gd_sns_policy.json           # SNS policy for message publishing
│   └── gd_lambda_policy.json        # Lambda execution permissions
├── .gitignore
└── README.md                        # Documentation
```

---

## **Setup Instructions**

### **Step 1: Clone the Repository**
Begin by cloning this repository to your local machine:
```bash
git clone https://github.com/yourusername/game-day-notifications.git
cd game-day-notifications
```

---

### **Step 2: Create an SNS Topic**
1. Log in to the **AWS Management Console** and navigate to the **SNS service**.
2. Click **Create Topic** and choose the **Standard** topic type.
3. Provide a topic name, such as `game-day-topic`, and click **Create Topic**.
4. Copy the Amazon Resource Name (ARN) of the topic for use in later steps.

---

### **Step 3: Subscribe Users to the SNS Topic**
1. Open the created topic and navigate to the **Subscriptions** tab.
2. Click **Create Subscription** and select a **Protocol**:
   - **Email**: Enter a valid email address and confirm the subscription via email.
   - **SMS**: Enter a valid phone number in international format (e.g., `+1234567890`).
3. Verify the subscription by clicking the confirmation link sent to the email address or confirming the SMS subscription.

---

### **Step 4: Set Up IAM Policies and Roles**
1. **Create IAM Policies**:
   - Navigate to **IAM Policies** in the AWS Management Console.
   - Use the `gd_sns_policy.json` file in the `policies/` directory to create a policy for SNS publishing.
   - Replace placeholders like `REGION` and `ACCOUNT_ID` with your AWS region and account ID.
2. **Create an IAM Role**:
   - Navigate to **IAM Roles** and create a role for Lambda execution.
   - Attach the following policies:
     - SNS Publish Policy (created earlier).
     - AWS Lambda Basic Execution Role (managed policy).
   - Copy the role ARN for use in the Lambda function.

---

### **Step 5: Deploy the Lambda Function**
1. Open the **AWS Lambda Console** and click **Create Function**.
2. Choose **Author from Scratch** and:
   - Enter a function name, such as `game_day_notifications`.
   - Set the runtime to **Python 3.x**.
   - Assign the IAM role created earlier.
3. Upload the code from `src/gd_notifications.py` or paste it directly into the inline editor.
4. Add environment variables:
   - `NBA_API_KEY`: Your SportsData.io API key.
   - `SNS_TOPIC_ARN`: The ARN of the created SNS topic.
5. Click **Create Function** to save the configuration.

---

### **Step 6: Schedule Notifications with EventBridge**
1. Open the **Amazon EventBridge Console** and create a rule:
   - Choose **Schedule** as the event source.
   - Set a cron expression for when notifications should be sent (e.g., hourly).
2. Add the Lambda function as the target for the rule.
3. Save and activate the rule.

---

### **Step 7: Test the System**
1. Navigate to the deployed Lambda function and create a test event.
2. Execute the test event and check the output in **CloudWatch Logs**.
3. Verify that notifications are delivered to the subscribed users via email or SMS.

---

## **Lessons Learned**
- Designed a scalable and serverless notification system using AWS services.
- Implemented least-privilege access for secure operation.
- Automated workflows using EventBridge for hands-free operation.
- Integrated external APIs into a cloud-based environment.

---

## **Future Enhancements**
1. **Additional Sports**: Expand the system to include alerts for NFL or other leagues.
2. **Personalized Alerts**: Use DynamoDB to store user preferences for specific teams or game types.
3. **User Interface**: Build a web interface for managing subscriptions and preferences.
4. **Enhanced Analytics**: Add reporting features for user engagement and notification performance.

---

### **Visual Assets**
- **Architecture Diagram**: Showcase the system's workflow.
- **AWS Console Screenshots**: Include images of SNS topic setup, Lambda configuration, and EventBridge rules.
- **CloudWatch Logs**: Display sample logs to illustrate system performance.

---

