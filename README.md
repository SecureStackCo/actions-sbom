# SecureStack SBOM

### What's an SBOM?
Software bill of materials (SBOM) are supposed to provide a list of ingredients that have gone into an application.  Having an SBOM allows you to know what you are getting and whether any of the ingredients have vulnerabilities.  This is why they are so important and why the US government has mandated that companies use them.  

### An application is more than just the third party libraries you are using
Its the source code, of course, but also the cloud resources, vendor dependencies and partner APIs you call.  If your application requires something to run, then it should be in the SBOM, right?  And that's why the SecureStack SBOM is created holistically from all the important components of your application.  This includes source code, third-party libraries and AWS cloud resources.  In addition, this SBOM will include any vulnerabilities from your source code and cloud stack.

```
name: Example Workflow Using SecureStack SBOM Action
on: push
jobs:
  security:
    runs-on: ubuntu-latest
    steps:
      - name: Create SBOM
        id: sbom
        uses: SecureStackCo/actions-sbom@v0.1.1
        with:
          securestack_api_key: ${{ secrets.SECURESTACK_API_KEY }}
          securestack_app_id: ${{ secrets.SECURESTACK_APP_ID }}
          severity: critical
```
NOTE - to understand possible values for the action input `flags`, run the SecureStack cli locally:

`$ bloodhound-cli SBOM --help`

## Create your SecureStack API Key and save as GitHub Secret

1. Log in to [SecureStack](https://app.securestack.com) with your GitHub credentials.
2. Go to Settings in the lower left corner, and then select the 6th tab: API.
3. Generate a new API key and copy the value.
4. Now back in GitHub, go to Settings for your GitHub repository and click on Secrets at the bottom left.
5. Create a new secret named SECURESTACK_API_KEY and paste the value from step 2 into the field.

## Retreiving your SecureStack Application ID

1. Log in to [SecureStack](https://app.securestack.com).
2. Open the application you wish to analyse.
3. In the browser URL bar you will see something like this: ```https://app.securestack.com/settings/applications/269aa3a5-9be8-1a23-1234-123456abcdef```
4. Copy the last part of that as the Application ID.  (ex: 269aa3a5-9be8-1a23-1234-123456abcdef)
5. Now go back to the GitHub UI and paste into the value of the `securestack_app_id` action input for the step using the SecureStack action in your workflow.

## What types of components will this BoM include?
1. All your software components including third-party libraries and frameworks
2. The AWS native resources that this application is actually using (think Ec2, S3, RDS, Cloudfront, ELB, CloudTrail, CloudWatch, Config, GuardDuty)

Made with 💜  by [SecureStack](https://securestack.com)
