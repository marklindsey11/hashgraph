# Run your mirror node using S3

## Requirements

* [AWS](https://aws.amazon.com/free/?trk=ps\_a131L0000085DvcQAE\&trkCampaign=acq\_paid\_search\_brand\&sc\_channel=ps\&sc\_campaign=acquisition\_US\&sc\_publisher=google\&sc\_category=core\&sc\_country=US\&sc\_geo=NAMER\&sc\_outcome=acq\&sc\_detail=aws%20account\&sc\_content=Account\_e\&sc\_segment=432339156165\&sc\_medium=ACQ-P|PS-GO|Brand|Desktop|SU|AWS|Core|US|EN|Text\&s\_kwcid=AL!4422!3!432339156165!e!!g!!aws%20account\&ef\_id=Cj0KCQjw8IaGBhCHARIsAGIRRYrLfWc3ykRf\_hAUeVvf4nNEYvacHwk\_w1jAuSj6hQZ8\_muh0T5p3acaAkZDEALw\_wcB:G:s\&s\_kwcid=AL!4422!3!432339156165!e!!g!!aws%20account\&all-free-tier.sort-by=item.additionalFields.SortRank\&all-free-tier.sort-order=asc\&awsf.Free%20Tier%20Types=\*all\&awsf.Free%20Tier%20Categories=\*all) account
* [Docker](https://www.docker.com/get-docker)
  * Check to see if you have it installed from your terminal: `docker --version && docker-compose --version`
  * For mirror node versions 0.35.0 and higher you will need docker v3.3.3+
* [Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)
* [Hedera Mirror Node Repository](https://github.com/hashgraph/hedera-mirror-node)&#x20;
  * You will be prompted to download the repo in the following steps&#x20;

## 1. Create an IAM user

{% hint style="info" %}
Create an IAM user with either an administrator or custom policy.
{% endhint %}

### **Administrator Policy**&#x20;

* Refer to AWS documentation to create an IAM user with administrator policy [here ](https://docs.aws.amazon.com/IAM/latest/UserGuide/getting-started\_create-admin-group.html)
  * This sets up an IAM user with Administrator Access Policy&#x20;
  * This user has full access and can delegate permissions to every service and resource in AWS.&#x20;
* Once that is complete, select **Users** from the left IAM navigation bar
* Select the **Administrator** from the **User name** column
* Select the **Security credentials** tab
* Select **Create access key**
* Copy or download your **Access key ID** and **Secret access key** &#x20;

### **Custom Policy**&#x20;

* Enable access to billing data
  * Follow step 2 [here](https://docs.aws.amazon.com/IAM/latest/UserGuide/getting-started\_create-admin-group.html)
* From the IAM left navigation bar select **Polices**&#x20;
* Click on **Create policy**
  * Service&#x20;
    * Enter **S3** as your service
  * Actions
    * Access level&#x20;
    * Select **List** and **Read**&#x20;
* Resources&#x20;
  * Select **Specify bucket resource ARN for the GetBucketLocation**&#x20;
  * Add ARN&#x20;
    * hedera-mainnet-streams&#x20;
  * Add ARN&#x20;
    * hedera-mainnet-streams/\*&#x20;
* Click **Next:Tags**
* Click **Next: Review**&#x20;
  * Enter a name for the policy
* Click **Create policy**&#x20;
* From the left navigation bar on the IAM console select **User** **Groups**&#x20;
* Click **Create group**&#x20;
* Enter a user group name
* Select the policy that was created in the previous step&#x20;
* Click **Create Group**&#x20;
* Click **Users** from the IAM console left navigation bar&#x20;
* Click on **Add user** &#x20;
* Enter username&#x20;
* Select **Programmatic access for Access type**&#x20;
* Click **Next: Permissions**&#x20;
* Select the group that was created in the previous step&#x20;
* Click **Next: Tags**&#x20;
* Click **Next: Review**&#x20;
* Click **Create user**&#x20;
* Copy or download your **Access key ID** and **Secret access key**&#x20;

## 2. Install the mirror node repository

```
git clone https://github.com/hashgraph/hedera-mirror-node.git
cd hedera-mirror-node/
```

## 3. Update the application.yml in the hedera-mirror-node directory

* `cd` into the `hedera-mirror-node` directory from your terminal or IDE
* Uncomment each field as shown below (except `gcpProjectId`) and update the `application.yml` file in the root folder with the following:

| Item              | Description                              |
| ----------------- | ---------------------------------------- |
| **accessKey**     | AWS access key                           |
| **cloudProvider** | s3                                       |
| **secretKey**     | AWS secret key                           |
| **network**       | Enter a network to run a mirror node for |

{% tabs %}
{% tab title="Sample application.yml file" %}
```
hedera:
  mirror:
    importer: 
      downloader:
        accessKey: ENTER ACCESS KEY HERE
        cloudProvider: "s3"
        secretKey: ENTER SECRET KEY HERE
#        gcpProjectId: For GCP only
      network: PREVIEWNET/TESTNET/MAINNET #Pick one network
```
{% endtab %}
{% endtabs %}

## 4. Run your mirror node

* From the `hedera-mirror-node` directory, run the following command:

```
docker-compose up
```

## 5. Access Your Beta Mirror Node Data

To access the mirror node data now available to you, enter the `hedera-mirror-node_db_1` container.

* Open a new terminal
* To view the list of containers, enter the following command:

```
docker ps
```

* Enter the following command to enter the `hedera-mirror-node_db_1` container

```
docker exec -it hedera-mirror-node_db_1 bash
```

* Enter the following command to access the database

```
psql "dbname=mirror_node host=localhost user=mirror_node password=mirror_node_pass port=5432"
```

* Enter the following command to view the complete list of tables

```
\dt
```

![](<../../.gitbook/assets/image (1) (1) (1) (1) (1) (1) (1) (1) (1).png>)

You have successfully deployed a Hedera mirror node :partying\_face: !
