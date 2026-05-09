
# Cloud Security with AWS IAM


**Author:** NightErth  

---

![Image](http://learn.nextwork.org/stimulated_azure_witty_bear/uploads/aws-security-iam_1c864649)

---

## Introducing Today's Project!

### Project overview

AWS IAM Access Control Project

In this project, I demonstrate how to use AWS Identity and Access Management (IAM) to control access and manage permission settings within an AWS account.

The goal of this project is to build a foundational understanding of cloud security by exploring how permissions and access policies are structured and enforced in AWS. Proper access control is a critical component of cloud infrastructure, as organizations must implement strict and well-defined permission models to protect resources and maintain security.

Throughout this project, I focus on the core concepts of IAM, including:

1. Creating and managing IAM users

2. Defining roles and permissions

3. Applying policies to control access to AWS services

By working through these fundamentals, the project highlights how companies implement secure access management practices in real-world cloud environments.

### Tools and concepts

Services Used:
Amazon EC2
AWS IAM

Key Concepts Learned:
IAM Users: Managing individual access to AWS resources.
IAM Policies: Defining permissions to control access.
IAM User Groups: Organizing users with similar access levels.
Account Aliases: Simplifying the AWS sign-in process with a custom alias.

Additional Skills Acquired:
Using the IAM Policy Simulator to test permissions in a controlled manner.
Understanding how JSON policies are structured and how they work in AWS.
Launching and managing EC2 instances.
Tagging instances for better organization and access control.
Logging into an AWS account using IAM credentials.

### Project reflection

This project took me approximately 2 hours to complete. The most challenging part was understanding IAM policies in JSON, especially since the policy contained multiple statements. However, it was incredibly rewarding to see the permission denied message when our intern attempted to delete the production instance. This confirmed that our IAM access management policy was working as intended, ensuring the security of our production environment.

---

## Tags

### What I did in this step

Launch EC2 Instances

In this step, we launch two Amazon EC2 instances to increase the computing capacity of the infrastructure. As the platform anticipates higher user activity and increased traffic during the summer period, additional compute resources are required to maintain performance and reliability.

By provisioning multiple EC2 instances, we ensure the system can better handle incoming requests and scale to support the expected growth in website usage.


### Understanding tags

Tags in AWS

Tags are metadata labels that allow you to organize and manage your AWS resources more effectively. By assigning tags to resources, you can group them based on various criteria, such as project, environment, or department.

Tags are particularly valuable for:

1. Resource Grouping: Easily categorize resources for better organization and management.

2. Cost Allocation: Track and allocate costs associated with specific resources or projects based on tag categories.

3. Policy Enforcement: Apply policies across all resources that share the same tag, enabling more efficient governance and security management.

By leveraging tags, AWS users can improve resource management, optimize cost allocation, and streamline access control and policy enforcement.

### My tag configuration

The tag I’ve used on my EC2 instances is called 'ENV'. The values I’ve assigned to my instances are 'Production' and 'Development.

This allows me to organize and manage my instances based on their environment, making it easier to implement specific policies, track costs, and maintain clear resource categorization.

![Image](http://learn.nextwork.org/stimulated_azure_witty_bear/uploads/aws-security-iam_2e0e5a5d)

---

## IAM Policies

### What I did in this step

In this step, we will use IAM policies to control the access levels for the new Network interns. These interns should have access to the development environment (i.e., the development instances) but not the production environment.

We will define a policy that grants permissions to the development resources while explicitly denying access to production resources. This ensures that the interns can work on non-critical resources without compromising the security of the production environment.

### Understanding IAM policies

IAM policies are rules that define who can perform what actions on specific resources within an AWS account. These policies specify the permissions granted to users, groups, or roles, determining which actions are allowed or denied on AWS resources. By leveraging IAM policies, you can enforce the principle of least privilege, ensuring that individuals and services have the minimum necessary access to perform their tasks.

We are using IAM policies to control who has access to our production environment instances. These policies will ensure that only authorized users or roles can interact with sensitive production resources, helping to maintain the security and integrity of the environment.

### The policy I set up

For this project, I’ve configured an IAM policy using JSON syntax. This policy defines the specific permissions and access controls required to manage access to resources within our AWS environment.

### Policy effect

We have created an IAM policy that grants the policy holder (i.e., the NextWork intern) the following permissions:

1. Full access to perform any action on instances tagged with 'development'.
2. Read-only access to view information for all instances, regardless of their tags.
3. Explicit denial of permissions to delete or create tags for any instance.

This policy ensures that the intern can work with development resources without being able to modify the tags or interact with production environments.

### Understanding Effect, Action, and Resource

Effect

The Effect element in an IAM policy defines whether a specific action is allowed or denied. It can have two possible values:

1. Allow: Grants permission for the specified action.
2. Deny: Explicitly denies permission, which takes precedence over any allow statements. Deny always overrides Allow.

For example, in the statement "Effect": "Allow", this indicates that the action is being permitted.


Action

The Action element specifies which actions are allowed or denied by the policy. This is a list of actions the policy can control.

For instance, "Action": "ec2:*" means that the policy allows all actions that can be performed on EC2 instances, including starting, stopping, and modifying instances. Essentially, it grants full control over EC2 resources.


Resource

The Resource element defines which resources the policy applies to. When the value is set to "*", it indicates that the policy applies to all resources within the defined scope.

---

## My JSON Policy

![Image](http://learn.nextwork.org/stimulated_azure_witty_bear/uploads/aws-security-iam_1c864649)

---

## Account Alias

### What I did in this step

In this step, we will set up an Account Alias, which serves as a user-friendly nickname for our AWS account console login. The account alias simplifies the login process, making it easier for users to access the AWS Management Console without needing to remember the full AWS account ID.

### Understanding account aliases

An Account Alias is a customizable nickname for your AWS account, providing a more user-friendly alternative to the long, numeric AWS Account ID. Instead of remembering the complex account ID, users can refer to the account by its alias, making it easier to access and manage the AWS Management Console.

### Setting up my account alias

Creating an Account Alias took just 20 seconds, as it’s a straightforward configuration in the IAM Dashboard. Now, my AWS console sign-in URL uses the newly created account alias instead of the long numeric AWS account ID, making the login process more convenient and user-friendly.

![Image](http://learn.nextwork.org/stimulated_azure_witty_bear/uploads/aws-security-iam_0eb4439b)

---

## IAM Users and User Groups

### What I did in this step

In this step, we will set up two key components: IAM Users and IAM User Groups.

1. IAM Users are individual logins for people who need access to our AWS account. Each user can be assigned specific permissions based on their role or function.

2. IAM User Groups act like organizational folders that help manage users with similar access levels. By grouping users together, we can apply permissions to the entire group, streamlining the management of access control.

### Understanding user groups

An IAM User Group is a collection, or "folder," of IAM users. It enables you to manage permissions for all users within the group simultaneously by attaching policies to the group itself, rather than applying them individually to each user. This simplifies the management of access control, especially when dealing with large numbers of users with similar roles or responsibilities.

### Attaching policies to user groups

We attached the NextWorkDevEnvironmentPolicy IAM policy, which we created earlier, to this user group. As a result, any user added to this group will automatically inherit the permissions defined in the NextWorkDevEnvironmentPolicy, ensuring consistent access control for all users within the group.

### Understanding IAM users

IAM Users are individuals or entities that are granted access to and can log in to our AWS account. Each IAM user represents a unique identity with specific permissions, allowing them to interact with AWS resources based on their assigned access rights.

---

## Logging in as an IAM User

### Sharing sign-in details

The first method is to email sign-in instructions directly to the user, providing them with the necessary details to log in. The second method is to download a .csv file, which contains the user's sign-in information, including the username and temporary password.

### Observations from the IAM user dashboard

Once logged in as the IAM user, we noticed that access to several panels in the AWS Management Console was already restricted. This is because we configured permissions specifically for the development EC2 instance, ensuring that the intern only has access to the resources related to development. As a result, they are unable to view or interact with any other resources in the console, including the production environment.

![Image](http://learn.nextwork.org/stimulated_azure_witty_bear/uploads/aws-security-iam_6f2ab446)

---

## Testing IAM Policies

### What I did in this step

In this step, we will log in to our AWS account as an intern to test access to both the production and development instances. This ensures that the intern has the appropriate permissions—limited only to what is necessary—while confirming they cannot perform any actions that could negatively impact the production environment.

### Testing policy actions

We tested our JSON IAM policy by attempting to stop both the production and development instances. 

### Stopping the production instance

When we attempted to stop the production instance, we encountered an error. This is because the production instance is tagged with the 'production' label, which falls outside the scope of the intern’s permission policy. As per the policy, interns are only authorized to interact with the development instances, ensuring they cannot make changes to production resources.

![Image](http://learn.nextwork.org/stimulated_azure_witty_bear/uploads/aws-security-iam_0e7a9d6a)

### Stopping the development instance

When we tried to stop the development instance, we successfully saw the instance state change to "initializing stopping" before it was fully stopped. This behavior occurs because our permission policy grants interns (i.e., NextWorks users in the dev group) full access to the development environment, including the ability to stop instances.

![Image](http://learn.nextwork.org/stimulated_azure_witty_bear/uploads/aws-security-iam_1811801c)

---

## IAM Policy Simulator

To extend our project, we will test our permission policy in a safer and more controlled manner using the IAM Policy Simulator. This approach allows us to validate the policy without disrupting our environment, as manually stopping instances and logging into other AWS accounts can be disruptive and time-consuming.

### Understanding the IAM Policy Simulator

The IAM Policy Simulator is a tool that allows us to simulate actions and test permissions by defining a specific user, group, or role, and the action we want to test. It's highly useful for saving time when validating permission settings, as it eliminates the need to log into other AWS accounts or stop instances. This enables us to test and refine policies in a more efficient and controlled manner.

### How I used the simulator

We set up a simulation to test whether our development user group had permissions to perform actions like StopInstances and DeleteTags. The results showed that both actions were denied. To resolve this, we adjusted the scope of the EC2 instances to only include those tagged with 'development'. Once we applied this tag, the permissions were successfully granted, as expected.

![Image](http://learn.nextwork.org/stimulated_azure_witty_bear/uploads/aws-security-iam_069d8a621)

---


