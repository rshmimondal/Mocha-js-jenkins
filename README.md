# How to integrate Jenkins pipeline for Mocha-js on [LambdaTest](https://www.lambdatest.com/?utm_source=github&utm_medium=repo&utm_campaign=Mocha-js-jenkins)

Jenkins Pipeline is also referred to as "Pipeline" offers a suite of plugins to help integrate your continuous delivery pipeline into Jenkins. Jenkins Pipeline does so with the help of Pipeline DSL(Domain Specific Language) syntax that facilitates easy modelling of even the most complex delivery pipeline. 

You can easily create a Jenkins pipeline for Mocha-js automation tests on LambdaTest using the following steps. You can refer to sample test repo [here](https://github.com/LambdaTest/mocha-selenium-sample).

## Prerequisites For Configuring Jenkins Pipeline With LambdaTest

1.  Jenkins 2.X or greater version.
2.  A Jenkins User with root access.
3.  Ensure you have the Pipeline plugin, although, it is displayed under the "suggested plugins" during the post-installation setup of Jenkins.
4.  **LambdaTest Authentication Credentials**
Be aware of your LambdaTest authentication credentials i.e. your LambdaTest username, access key and HubURL. You need to set them up as your environment variables. You can retrieve them from your  **[LambdaTest automation dashboard](https://automation.lambdatest.com/)**  by clicking on the key icon near the help button.

-   For Linux/Mac:
    
    ```
    $ export LT_USERNAME= {YOUR_LAMBDATEST_USERNAME}$ export LT_ACCESS_KEY= {YOUR_LAMBDATEST_ACCESS_KEY}
    ```
    
-   For Windows:
    
    ```
    $ set LT_USERNAME= {YOUR_LAMBDATEST_USERNAME}$ set LT_ACCESS_KEY= {YOUR_LAMBDATEST_ACCESS_KEY}
    ```
## Setting Up Jenkins Pipeline

Find the code for setting up a pipeline for the sample Mocha-js repo.
```bash
pipline 
{
    withEnv(["LT_USERNAME=Your LambdaTest UserName",
    "LT_ACCESS_KEY=Your LambdaTest Access Key",
    "LT_TUNNEL=true"]){

    echo env.LT_USERNAME
    echo env.LT_ACCESS_KEY 

    stages{
        stage('setup') { 

            // Get some code from a GitHub repository
            try{
            git 'https://github.com/LambdaTest/mocha-selenium-sample'

            //Download Tunnel Binary
            sh "wget https://s3.amazonaws.com/lambda-tunnel/LT_Linux.zip"

            //Required if unzip is not installed
            sh 'sudo apt-get install --no-act unzip'
            sh 'unzip -o LT_Linux.zip'

            //Starting Tunnel Process 
            sh "./LT -user ${env.LT_USERNAME} -key ${env.LT_ACCESS_KEY} &"
            sh  "rm -rf LT_Linux.zip"
            }
            catch (err){
            echo err
        }

        }
        stage('build') {
            // Installing Dependencies
            sh 'npm i'
            }

        stage('test') {
                try{
                sh 'npm run single'
                }
                catch (err){
                echo err
                }  
        }
        stage('end') {  
            echo "Success" 
            }
        }
    }
}

```
You can now add this script when creating the pipeline by using the following steps:

1. Create new pipleline
2. Scroll down to Advanced Project Options.
3.  Paste the Code in the code pane or fetch it via SCM & hit the **Save** button.

**Note:**  To run on the tunnel, Either you can use LT_TUNNEL Environment variable to set the tunnelling capability or you can pass in the code. Instructions on the tunnel are are available in the sample repo readme.



## Additional Links

* [Advanced Configuration for Capabilities](https://www.lambdatest.com/support/docs/selenium-automation-capabilities/)
* [How to test locally hosted apps](https://www.lambdatest.com/support/docs/testing-locally-hosted-pages/)
* [How to integrate LambdaTest with CI/CD](https://www.lambdatest.com/support/docs/integrations-with-ci-cd-tools/)

## Tutorials 📙

Check out our latest tutorials on JavaScript automation testing 👇

* [How To Generate Mocha Reports With Mochawesome?](https://www.lambdatest.com/blog/how-to-generate-mocha-reports-with-mochawesome/)
* [Mocha JavaScript Tutorial With Examples For Selenium Testing](https://www.lambdatest.com/blog/mocha-javascript-tutorial-with-examples-for-selenium-testing/)

## Documentation & Resources :books:
      
Visit the following links to learn more about LambdaTest's features, setup and tutorials around test automation, mobile app testing, responsive testing, and manual testing.

* [LambdaTest Documentation](https://www.lambdatest.com/support/docs/?utm_source=github&utm_medium=repo&utm_campaign=Mocha-js-jenkins)
* [LambdaTest Blog](https://www.lambdatest.com/blog/?utm_source=github&utm_medium=repo&utm_campaign=Mocha-js-jenkins)
* [LambdaTest Learning Hub](https://www.lambdatest.com/learning-hub/?utm_source=github&utm_medium=repo&utm_campaign=Mocha-js-jenkins)    

## LambdaTest Community :busts_in_silhouette:

The [LambdaTest Community](https://community.lambdatest.com/) allows people to interact with tech enthusiasts. Connect, ask questions, and learn from tech-savvy people. Discuss best practises in web development, testing, and DevOps with professionals from across the globe 🌎

## What's New At LambdaTest ❓

To stay updated with the latest features and product add-ons, visit [Changelog](https://changelog.lambdatest.com/) 
      
## About LambdaTest

[LambdaTest](https://www.lambdatest.com/?utm_source=github&utm_medium=repo&utm_campaign=Mocha-js-jenkins) is a leading test execution and orchestration platform that is fast, reliable, scalable, and secure. It allows users to run both manual and automated testing of web and mobile apps across 3000+ different browsers, operating systems, and real device combinations. Using LambdaTest, businesses can ensure quicker developer feedback and hence achieve faster go to market. Over 500 enterprises and 1 Million + users across 130+ countries rely on LambdaTest for their testing needs.    

### Features

* Run Selenium, Cypress, Puppeteer, Playwright, and Appium automation tests across 3000+ real desktop and mobile environments.
* Real-time cross browser testing on 3000+ environments.
* Test on Real device cloud
* Blazing fast test automation with HyperExecute
* Accelerate testing, shorten job times and get faster feedback on code changes with Test At Scale.
* Smart Visual Regression Testing on cloud
* 120+ third-party integrations with your favorite tool for CI/CD, Project Management, Codeless Automation, and more.
* Automated Screenshot testing across multiple browsers in a single click.
* Local testing of web and mobile apps.
* Online Accessibility Testing across 3000+ desktop and mobile browsers, browser versions, and operating systems.
* Geolocation testing of web and mobile apps across 53+ countries.
* LT Browser - for responsive testing across 50+ pre-installed mobile, tablets, desktop, and laptop viewports
    
[<img height="58" width="200" src="https://user-images.githubusercontent.com/70570645/171866795-52c11b49-0728-4229-b073-4b704209ddde.png">](https://accounts.lambdatest.com/register)
      
## We are here to help you :headphones:

* Got a query? we are available 24x7 to help. [Contact Us](support@lambdatest.com)
* For more info, visit - [LambdaTest](https://www.lambdatest.com/?utm_source=github&utm_medium=repo&utm_campaign=Mocha-js-jenkins)
