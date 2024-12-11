---
published: true
type: workshop
title: GitHub Copilot Hands-on Lab 
short_title: GitHub Copilot Hands-on Lab
description: Discover how to leverage GitHub Copilot to develop your project
level: beginner
authors:
  - Ruka Sakurai
contacts:
  - '@rukasakurai'
duration_minutes: 60
tags: javascript, .net, GitHub, copilot, AI, csu
#banner_url: assets/banner.jpg           # Optional. Should be a 1280x640px image
#video_url: https://youtube.com/link     # Optional. Link to a video of the workshop
#audience: students                      # Optional. Audience of the workshop (students, pro devs, etc.)
#navigation_levels: 2                    # Optional. Number of levels displayed in the side menu (default: 2)
#navigation_numbering: true             # Optional. Enable numbering in the side menu (default: true)
#sections_title:                         # Optional. Override titles for each section to be displayed in the side bar
#   - Section 1 title
#   - Section 2 title
---

# GitHub Copilot Hands-on Lab
This hands-on lab is intended as material that can be used as the first step in learning how to use GitHub Copilot. The "First steps with GitHub Copilot" and "User GitHub Copilot Chat to imporve code quality" and "Prompt engineering in GitHub Copilot Chat" sections are recommended for everyone. The intent for the following programming language dependent sections are so that users can choose and prioritize depending on the intended use case.

This workshop can be acccessed from the following URL: https://aka.ms/ws?src=gh:rukasakurai/github-copilot-tutorial/main/docs/

## Required pre-requisites
- Internet access
- [Microsoft Edge](https://www.microsoft.com/edge) or Google Chrome
- [VS Code](https://code.visualstudio.com/Download)
- GitHub account
- GitHub Copilot access
- [Set up GitHub Copilot in VS Code](https://code.visualstudio.com/docs/copilot/setup)

## Optional pre-requisites
- [GitHub Copilot for Azure](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-azure-github-copilot)
- [Node.js](https://nodejs.org)
- [.Net Core](https://dotnet.microsoft.com/download)
- [Python](https://www.python.org/downloads/)

## Sample commands for checking
```bash
code --version
code --list-extensions | grep 'github.copilot'
node --version
dotnet --version
python --version
```

---

# GitHub Copilot overview
GitHub Copilot is an AI coding assistant that helps you write code faster and with less effort, allowing you to focus more energy on problem solving and collaboration.

## GitHub Copilot features
Code Completion and Copilot Chat are the two most commonly used features of GitHub Copilot, and this hands-on lab will mainly cover these features.

For additional features please check 
https://docs.github.com/en/copilot/about-github-copilot/github-copilot-features

---

# Code Completion

This section will guide you through the first steps with GitHub Copilot.

## Get ready

Clone the following GitHub Repository: [Github Copilot Demo](https://github.com/Philess/gh-copilot-demo)

This repository is a code starter that will help you experiment with the capabilities of GitHub Copilot.

``` bash
git clone https://github.com/Philess/gh-copilot-demo
cd gh-copilot-demo
code .
```

## GitHub Copilot shortcuts in VS Code
Use shortcuts to interact with GitHub Copilot.

Refer to 
https://docs.github.com/en/copilot/managing-copilot/configure-personal-settings/configuring-github-copilot-in-your-environment

<div class="tip" data-title="tip">

> If you can't remember the shortcuts, hover your pointer on top of a suggestion to make the most commonly used shortcuts to appear.

</div>

## Code completion

Open file `album-viewer/lang/translations.json`

```json
[
    {
        "language": "en",
        "values": {
            "main-title": "Welcome to the world of the future",
            "main-subtitle": "The future is now with copilot",
            "main-button": "Get started"
        }
    }
]
```

- Start adding a new block by adding a "," after the last "}" and press enter

<br>

## Code from comment generation

**Generate code from a comment**

Create a new `album-viewer/utils/validators.ts` file and start with the prompt:

```ts
// validate date from text input in french format and convert it to a date object
```

GitHub Copilot can help you also to write `RegExp patterns`. Try these:

```ts
// function that validates the format of a GUID string

// function that validates the format of a IPV6 address string
```

<br>

**Explore alternative suggestions**

Still on the same `album-viewer/utils/validators.ts` file add the following prompt:

```ts
// validate phone number from text input and extract the country code
```

<div class="info" data-title="info">

> For this one it will probably give you proposal that call some methods not defined here and needed to be defined. It's a good opportunity to explore the alternatives using the `ctrl+enter` shortcut to display the GitHub Copilot pane.

</div>

**Additional examples**

In the `albums-api/Controllers/AlbumController.cs` file try to complete the `GetByID` method:

```cs
// GET api/<AlbumController>/5
[HttpGet("{id}")]
public IActionResult Get(int id)
{
    //here
}
```

In the same file you can show other prompts like:

```cs
// function that search album by name, artist or genre

// function that sort albums by name, artist or genre
```

## Big tasks vs small tasks

### Big Prompts and Short Prompts

GitHub Copilot is more effective with prompts that are intendend to generate small pieces of code rather than a large chunks of code.

<div class="tip" data-title="tip">

> The best strategy to generate big piece of code, is by adding small pieces one by one.

</div>

**Big prompts that *could* works**

- Back in the `albums-viewer/utils` add a new file `viz.ts` to create a function that generates a graphe. Here is a sample of prompt to do that:

```ts
// generate a plot with D3.js of the selling price of the album by year
// x-axis are the month series and y-axis show the numbers of album selled
// data from the sales of album are loaded in from an external source and are in json format
```

<div class="info" data-title="info">

>GitHub Copilot will probably try to complete the prompt by adding more details. You can try to add more details yourself or follow GitHub Copilot's suggestions. When you want it to stop and start generating the code just jump on another line and let the GitHub Copilot do its work.

</div>

- Once you achieved to generate the code for the chart you might see that your IDE warns you about the d3 object that is unknown. For that also GitHub Copilot helps.
Return on top of the file and start typing `import d3` to let GitHub Copilot autocomplete

```ts
import d3 from "d3";
```

Look at what GitHub Copilot has been able to generate. It's possible that the code is working fine and does everything you asked for but also you probably hit the token limit and GitHub Copilot was not able to generate the whole code.

It's because GitHub Copilot for autocompletion is not made for creating big pieces of code at once, but is more specialized in generating small pieces step by step.

**Try again by build it step by step**

Try to generate the code for the plot by cutting it into small pieces following the steps below:

```ts
import * as d3 from 'd3';

// load the data from a json file and create the d3 svg in the then function
```

Inside the then function, starts by setting up the basics of the plot

```ts
// create the svg
```

```ts
// create the scales for the x and y axis
// x-axis are the month series and y-axis show the numbers of album selled
```

```ts
// create axes for the x and y axis
```

From there you can just ask to GitHub Copilot to complete the chart

```ts
// generate a line chart based on the albums sales data
```

<div class="tip" data-title="tip">

>You will **always** get better results by cutting big task into small chunks with GitHub Copilot autocomplete. It's also a good way to show that GitHub Copilot is not magic and you have to use it with your other IDE feature and your developer logic.

</div>

## Tests

GitHub Copilot can help generate all kind of tests that are written with code. It Includes `unit tests, integration tests, end to end tests, and load testing` tests with JMeter scripts for example.

- Add a new file `validators.test.ts` in the `albums-viewer/tests` folder

- To have good test suggestion, you hould provide some basic informations to GitHub Copilot such as the test framework you want to use:

```ts
import { describe }
```

When you start typing the `describe` function, GitHub Copilot will see you're in test file in TS and suggest you to import the `describe` and `it` functions from Mochai which is a famous test framework for JS/TS.
Accept the suggestion and it will automatically suggest also the `expect` function from Chai: accept it also.

```ts
import {describe, it} from 'mocha';
import {expect} from 'chai';
```

You have your test framework in place! Now just import the functions you want to test by starting a new line by `import` keyword GitHub Copilot will see you are in a test file, to test some `validators` because of the name and it will suggest something like that:

```ts
import {validateAlbumId} from '../src/validators';
```

It looks ok but because GitHub Copilot doesn't have access to all your code, only the open tab and limited informations, you can see that both the path and the function name are wrong.
It's a good way to show that GitHub Copilot is not magic and you have to use it with your other IDE feature and your brain.

- Accept the suggestion and change the path. You will be able to have VS Code give you the available function with the `ctrl+space` shortcut.

- Add a comment with the first function you want to test and let the magic happen:

```ts
import {describe, it} from 'mocha';
import {expect} from 'chai';

import {validateDate, validateIPV6} from '../utils/validators';

// test the validataDate function
```

Boom!

```ts
describe('validateDate', () => {
    it('should return a date object when given a valid date string', () => {
        const date = '01/01/2019';
        const expectedDate = new Date(2019, 0, 1);
        expect(validateDate(date)).to.deep.equal(expectedDate);
    });

    it('should throw an error when given an invalid date string', () => {
        const date = '01/01/2019';
        expect(() => validateDate(date)).to.throw();
    });
});
```

*You can add other `it` block to add more test cases and also add the tests for the other functions. For example try add a new `it` block for the validateDate function to test that it throws and error when given en empty string.*

## Writing CI pipelines

*GitHub Copilot will help you in writing your pipeline definition files to generate the code for the different steps and tasks. Here are some examples of what it can do:*

- *generate a pipeline definition file `from scratch`*
- *accelerate the writing of a pipeline definition file by `generating the code` for the different `steps, tasks and pieces of script`*
- *help `discover marketplace tasks and extensions` that match your need*

### Step 1: generate from scratch

- Create a new file `pipeline.yml` in the `.github/workflows` folder of the project and start typing the following prompt:

```yml
# Github Action pipeline that runs on push to main branch
# Docker build and push the album-api image to ACR
```

*GitHub Copilot will generate the pipeline block by block. Generation pipelines Yaml, you will sometimes need to jump to a new line to trigger the generation of the next block more often than with other type of code.*

*It will often generate a task with a few errores coming from bad indentation or missing quote around a task name. You can easily fix these with your IDE and your developer skills :)*

### Step 2: add tasks from prompts

- You probably have a github action workflow with at least a "login" task to your container registry and a "docker build and deploy" task. Add a new comment after those tasks to tag the docker image with the github run id and push it to the registry:

```yml
# tag the image with the github run id and push to docker hub
```

you can play with other prompts like:

```yml
# run tests on the album-api image

# deploy the album-api image to the dev AKS cluster
```

### Step 3: add scripts from prompts

- GitHub Copilot is also very usefull when you need to write custom script like the following example:

```yml
# find and replace the %%VERSION%% by the github action run id in every appmanifest.yml file
```

## Infrastructure-as-code

GitHub Copilot can also help you write infrastructure-as-code (e.g., Bicep)

Open the `main.bicep`file in `iac/bicep` folder and start typing prompts at the end of the file to add new resources:

```js
// Container Registry

// Azure Cognitive Services Custom Vision resource
```

## Generate Git Commit comment

Yes, writing a comment should be mandatory and developers tend to be lazy. GitHub Copilot can help with that.

1. Just edit any file by adding some relevant content into it.

2. On the Git commit panel, click the small magical button on the right

    ![GitHub Copilot Git comment generator](assets/git-commit.png)

3. Admire GitHub Copilot having generated a comment for you

    ![Generated comment(assets/git-commit2.png)

## Writing documentation

GitHub Copilot can understand a natural language prompt and generate code and because it's just language to it, it can also `understand code and explain it in natural language` to help you document your code.
So it can help you in all your documentation tasks. It can generate simple documentation comment or standardized documentation comment like JavaDoc, JsDoc, etc... it can also help you translate your documentation in different languages. Let's see how it works.

### simple documentation comment

To see that just put you pointer on top of a Class, a method or any line of code and start typing the comment handler for the selected language to trigger GitHub Copilot. In language like Java, C# or TS for example, just type `// `and let the magic happen.

Here is an example in the `albums-viewer/routes/index.js` file. Insert a line and start typing on line 13 inside the `try block`

```js
router.get("/", async function (req, res, next) {
  try {
    // Invoke the album-api via Dapr
    const url = `http://127.0.0.1:${DaprHttpPort}/v1.0/invoke/${AlbumService}/method/albums`;

```

Continue to play with it and see what happens on other pieces of code.

### standardized documentation comment (JavaDoc, JsDoc, etc...)

For this one, to trigger the documentation comment generation, you need to respect the specific comment format:

-  `/**` (for JS/TS) in the `index.js` file for example
- `///` for C# in the `AlbumController.cs` of the AlbumApi file for example

```cs
/// <summary>
/// function that returns a single album by id
/// </summary>
/// <param name="id"></param>
/// <returns></returns>
[HttpGet("{id}")]
public IActionResult Get(int id)
```

### Writing markdown and html documentation

GitHub Copilot is also very powerfull to help you write documentation. It can generate `markdown` and `html` code and accelerate the writing of your readme.md files like for this one for example.

You can show that by creating a new file `demo.md` in the root of the project and start typing the following prompt:

```md
# Github Copilot documentation
This documentation is generated with Github Copilot to show what the tool can do.

##
```

From there by starting a new line with a secondary level title it will start generating the content of the documentation and it will showcase how it will accelerate the documentation writing process.

---

# GitHub Copilot Chat

GitHub Copilot is a generative AI and thus, perfect to generate code, but it has powerfull analysis capabilities on your code that can be used in several case to improve code quality like: find security issues, bad practices in your code and générate a fix, refactor and add comment to legacy code, generate tests, etc...

If you already feel confortable with it you can jump to the next section.

## Let's Start

To start using Github Copilot Chat, you first need to:

- Have a valid GitHub Copilot license (personal, business or enterprise).
- Install the extension in your IDE. For VS Code, you can find it directly by searching for `Github Copilot Chat` in the extensions tab.

### Clone the repository

We will use the same repository as the previous section to show how to use GitHub Copilot Chat to improve code quality. If you already have it, you can skip this step.

You need to clone the following GitHub Repository: [Github Copilot Demo](https://github.com/Philess/gh-copilot-demo)

This repository is a code starter that will help you experiment all capabilities with GitHub Copilot. Take the time to look at the architecture design displayed on the page and when you're ready, clone the repository from the command line and open it in VS Code.

``` bash
git clone https://github.com/Philess/gh-copilot-demo
cd gh-copilot-demo
code .
```

## Start playing with the Chat

Once GitHub Copilot Chat is setup, you can start using it:

- by accessing the **chat view** from the left toolbar of your IDE (chat icon)
- by pressing `Ctrl` + `Shift` + `i` shortcut for a quick **inline question** to the chat

The first one is a sticky version, very usefull to keep the chat open and ask questions to copilot.
The second one is a quick way to ask a question and get an answer and launch commands.

### Chat View

The chat view gives you a full chat experience, integrate as any other tool view in your IDE. Once the view is open you can start chatting with GitHub Copilot as your personnal code coach. It keeps the history of the conversation and you can ask question related to the previoius answers. It also provides suggestions for questions along the way. You can:

- ask general question about coding on any language or best practice
- ask to generate or fix code related to the current file and inject the code directly in the file

It's a more high level copilot than the vanilla GitHub Copilot which is specialized on providing code completion.

Try it with a few questions like:

```text
> How to generate a random number in C#?
> What is the best way to secure a route is ASP.NET Core?
> What is the easiest way to generate a static website with NodeJS?
```

Try it then with some of your code files in the repository. Open a file a try asking:

```text
> Can you explain me what this code does?
> (with only part of the code selected) Can you explain me what the selected code does?
> Can you generate a function that returns a random number between 1 and 10?
> Can you add documentation commentes to this function?
```

Try also using the questions suggestions that appears along the way.

### Inline question

The inline question is a quick way to ask a question to GitHub Copilot and get an answer. It's a good way to ask a question about a specific piece of code. It's also a good way to launch commands to GitHub Copilot. You can ask it to generate code, fix code, generate tests, etc...

try it by pressing `Ctrl` + `Shift` + `i` and type the same type of commands you tried in the chat view.

### Slash Commands

To further help GitHub Copilot give you more relevant answers, you can choose a topic for your questions through "slash commands."

You can prepend your chat inputs with a specific topic name to help GitHub Copilot give you a more relevant response. When you start typing /, you’ll see the list of possible topics:

- **/explain**: Explain step-by-step how the selected code works.
- **/fix**: Propose a fix for the bugs in the selected code.
- **/help**: Prints general help about GitHub Copilot.
- **/tests**: Generate unit tests for the selected code.
- **/vscode**: Questions about VS Code commands and settings.
- **/clear**: Clear the session.

## Secure your code

GitHub Copilot can help you find security issues in your code and fix them. It can also help you find bad practices in your code and fix them. Let's see how it works.

Open the `album-api/Controllers/UnsecuredController.cs` file and type questions like these to the chat:

```text
> Can you check this code for security issues?
> Do you see any quality improvement to do on this code?
```

Once you have the answer, you can ask to fix the issues by typing:

```text
> Can you propose a fix?
```

When you have the fix in the code you choose to **copy it or inject it directy in the file** by hovering the code block in the chat and selecting the right option on the top left.

## Code Explanation and documentation

You can use GitHub Copilot Chat to explain code to you. It can `explain you the code in natural language or generate documentation comments for you`. Let's try that with the following commands:

```test
> /explain
> Generate documentation comments for this code
```

## Code Refactoring

More impressive, GitHub Copilot chat can help you refactor your code. It can help you `rename variables, extract methods, extract classes, etc...`.

You can try some of these commands on the `album-api/Controllers/UnsecuredController.cs` file:

```test
> extract methods
> create Async version of each methods when it makes sense
```

## Code Translation

*GitHub Copilot can understand and generate natural languages and code language in both way so by combining everything you can use it to `translate code pieces from a language to another one`*

To translate a piece of code in a specific language, open it and ask to the chat to translate it to another language. For example open the `validators.ts` file created in the first section dedicated to GitHub Copilot autocompletion and ask to translate it to C for example.

In case of dealing with Legacy code like COBOL for example it can be very useful. Open the `legacy/albums.cbl` file and try translating the code to Python.

## Tests generation

GitHub Copilot can also help you generate tests for your code. It can generate `unit tests, integration tests, end to end tests, and load testing` tests with JMeter scripts for example.

Open the `album-api/Controllers/UnsecuredController.cs` file and type questions like these to the chat:

```test
> Generate a unit tests class for this code
```

You can also use GitHub Copilot to help you generate stubs and mocks for your tests.

```text
> Generate a mock for FileStream class
> Use that mock in the unit tests
```

<div class="info" data-title="note">

> Remember that GitHub Copilot chat is keeping track of the previous Q & A in the conversation, that's why you can reference the previously generated mock and test easily.

</div>

## Use Chat participants

Chat participants are like specialized experts who can assist you with specific tasks. You can mention them in the chat using the @ symbol. Currently, there are three Chat participants available for Visual Studio Code:

- **@workspace**: This chat participant has knowledge about the code in your workspace and can help you navigate it by finding relevant files or classes. The @workspace chat participant uses a meta prompt to determine what information to collect from the workspace to help answer your question.
- **@vscode**: This chat participant is knowledgeable about commands and features in the VS Code editor itself, and can assist you in using them.
- **@terminal**: This chat participant has context about the Visual Studio Code terminal shell and its contents.
- **@azure**: Thit chat participant is designed to help streamline the process of developing with Azure.

Open the side Chat panel and type **@workspace /New* to specify that you want to create a new project. For instance, try to create an Asp.Net project

```text
> @workspace /new create a new asp.net core 6.0 project, with three views Index, Users and products.
```

It should create a structured project and even a new button to create the file. Click on "Create workspace" to see files being created.

![GitHub Copilot Chat Participants](assets/agents.png)

### GitHub Copilot for Azure (`@azure`)
With GitHub Copilot for Azure (`@azure`), you can have a conversation with GitHub Copilot that uses information about your Azure environment. It is useful in scenarios such as resource management, diagnostics, cost management, etc.

To use GitHub Copilot for Azure (`@azure`), you will need to install the extension: 
https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-azure-github-copilot

#### Sample prompts
`@azure What can you do?`
If you are not signed into Azure, this will prompt you to signin.

For additional prompts, refer to: https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-azure-github-copilot

## Tips

For a developer, leaving the keyboard and having to take the mouse to open the Chat tab can be inconvenient. You can directly call the Chat inside the code editor.

1- Open any file containing code
2- Use the shortcut **Ctrl + i**. It should open the Quick chat popup, a small chat windows where you put your cursor
3- Type any command to generate some code (i.e. "Create a C# class named Toto). The generated code is injected inside the current file which may be what you want

---

# Prompt engineering in GitHub Copilot Chat

In the previous section you discovered how to use basic prompts to get code from GitHub Copilot Chat. In this section you will learn techniques to get more accurate results using prompt engineering techniques.

**What is prompt engineering?**
Prompt engineering is the process of designing high quality prompts to generate high quality code suggestions. There are good practices and tips to write better prompts. Let's see some of them.

## Provide examples: one-shot and few-shots programming

Talking about prompt engineering, you can also use the chat to provide examples to GitHub Copilot. It's a good way to help GitHub Copilot understand what you want to do and generate better code. You can provide examples in the chat by typing with the validator.ts file open:

```bash
# one-shot programming

Write me unit tests for phone number validators methods using mocha and chai in the current file.
Use the following examples for positive test (test that should return true): 
it('should return true if the phone number is a valid international number', () => { expect(validatePhoneNumber('+33606060606')).to.be.true; });
Organize test in logic suites and generate at least 4 positives tests and 2 negatives tests for each method.
```

```bash
# few-shot programming

Write me unit tests for all validators methods using mocha and chai in the current file.
Use the following examples for positive test (test that should return true): 
it('should return true if the phone number is a valid international number', () => { expect(validatePhoneNumber('+33606060606')).to.be.true; });
it('should return true if the phone number is a valid local american number', () => { expect(validatePhoneNumber('202-939-9889')).to.be.true; });
it('should throw an error if the given phone number is empty', () => { expect(validatePhoneNumber('')).to.throw(); });
Organize test in logic suites and generate at least 4 positives tests and 2 negatives tests for each method.
```

You can use this technique to **generate code that keeps the styling code from another file**. For example if you want to create sample records for music style like the Albums in albums-api>Models>Album.cs file, open it and type:

```bash
Write a MusicStyle record that conatins a List<MusicStyle> with 6 sample values like in the Album.cs file.
```

## Provide external references

The chat GitHub Copilot can use external references to build more accurate suggestions. For exemple if you want to generate a code that make a request to an API you can provide an example of the API response in the chat or the url to the API reference. GitHub Copilot will use it to generate better code.

```bash
Write a TS function that retreieves all dog breeds from the following API and return an array of Breed objects Request: HTTP GET https://dog.ceo/api/breeds/list/all
```

GitHub Copilot will use the given external reference to generate the code. You will see that he wil generate the Breed interface (or class) with a subBreeds property. It's coming from the API given by the external reference.

```ts
interface Breed {
  name: string;
  subBreeds: string[];
}
```

<div class="tips" data-title="tip">

> You can also provide links to external documentations like SDK, libraries, etc... or event normative documents like RFCs, etc...

</div>

## Role Prompting

Also called foundational prompt, it's a general prompt you're giving to GitHub Copilot Chat to personnalise his behavior and setup your flavour of GitHub Copilot.

This is probably the first thing to do when you start a new task with GitHub Copilot Chat: **provide a clear description of what you want to build and how do you want GitHub Copilot to help you**.

<div class="warning" data-title="Important">

> **This is very powerfull when handled properly** so be sure to start every coding sessions with a role prompt and save your best prompt for future use.

</div>

***Structure of a role prompt***

What can you include in a role prompt:

- Provide solid context and background information on what you want to build.
- Define GitHub Copilot’s role and setting expectations about what feedback we are looking for.
- Be specific in the quality of answers and ask for reference and additional resources to learn more and ensure the answers you receive are correct
- Resume the task and ask if the instructions are clear

***Example of a role prompt***

Start a new conversation and type the following prompt:

```bash
I'm working on a new mobile application that is built on React Native. 
I need to build a new feature that will allow the user to upload a picture of a dog and get the breed of the dog. 
I will need to use the following set of APIs to work on the breeds: https://dog.ceo/api/breeds. I need to be sure that my code is secured againt at least the OWASP Top 10 treats (https://owasp.org/Top10/). 
I need to have unit tests for the code and i want my application to be fully accessible and conforms with the WCAG 2.1 level A and AA success criteria defined at https://www.w3.org/TR/WCAG21/.
I need you to act as my own code coach to ensure that my code fits all these requirements. 
When possible, please provide links and references for additional learning. 
Do you understand these instructions? 
```

From there you can start asking questions and from time to time, ensure GitHub Copilot still follows the instructions by asking:

```bash
Are you still using the instructions I provided?
```

***Test your role prompt***

You can test your role prompt by asking questions about best practices for accessibility on React Native Apps and OWASP Top 10 treats. You can also ask to generate code for the upload feature and check if the generated code is secured and accessible.

Try these questions for example:

```bash
how can i make my app accessible with react native?

what is the most secure way to upload a photo from my app?
```

---

# Lab: Pytorch

In this exercise, you are going to develop and test a computer vision model using Pytorch

## Clone the sample repository
```
git clone https://github.com/rukasakurai/object-detection
```

## Use GitHub Copilot Chat to get an overview of the current code
```text
Look that the directory and file structure of this repository and explain what it is for
```

## Pytorch completions
### Training code
Open file `src/train.py`

Select the code and in GitHub Copilot Chat ask "@workspace /explain concisely"

Play around with other GitHub Copilot capabilites.

### Inference code

Open file `src/train.py`

Select the code and in GitHub Copilot Chat ask "@workspace /explain concisely"

Play around with other GitHub Copilot capabilites.

## Infrasturcture-as-code
While Pytorch model training and inference can be performed on a local machine, it is often useful to leverage cloud resources. These cloud resources can be provisioned using the GUI, but leveraging infrastructure-as-code is often preferrable from the perspective of repeatability and teamwork.

### Ask @azure for recommended Azure resources
```text
@azure What Azure resources do you recommend that I use for training and inference using PyTorch?
```

### Use GitHub completions to create infrastructure-as-code
```bicep
# Azure Machine Learning resource for training and testing
```

```bicep
# Azure Container Apps for hosting the PyTorch model
```

---

# Lab: Node.js

In this exercise, you are going to develop a real project following functional requirements. You can do it by yourself or...with the help of GitHub Copilot.

## Instructions

- Download to local the [exercicefile](assets/src/exercisefiles.zip) folder
- Open `nodeserver.js` and begin by writing a Nodejs server, check the first suggestions based on the initial text
- Open `test.js` file and analyze the current test
- Open a command prompt and run the test (`mocha test.js`)
- See the result, it should display something like:

``` bash
mocha test.js
server is listening on port 3000

  Node Server
    
    √ should return "key not passed" if key is not passed

  1 passing (34ms)

```

- In the `nodeserver.js` develop the rest of the methods described in the Exercise described in the section below
  
> Do not forget to open `color.json` file in Visual Studio Code, so GitHub Copilot get all the context to make better recommendations

- In the test.js file add the methods to test the functionality
- Run the tests to verify that all is working
- Open the `dockerfile` file, and fill it, to create a docker container with a node image that can run the web server
- Create a command to run docker in port 4000
- Test that the application is working in port 4000
- In the **nodeserver.js** file, you can type a new line like `//run a curl command to test the server` so we can see how GitHub Copilot based on the current file produces a curl command, to be executed in the command line.
- Note: you can be more specific like `//run a curl command to test the daysBetweenDates` method. It should generate a test for a specific method

## Exercise

You must now develop and add new features to your server. The requests that the server must attend are the following:

<div class="tip" data-title="tip">

> As you type GitHub Copilot will make suggestions, you can accept them by pressing Tab. If nothing shows up after GitHub Copilot write some lines, press enter and wait a couple of seconds. On Windows or Linux, press Ctrl + Enter.

</div>

<div class="info" data-title="note">

> There are a lot of code to write but you may be surprised by the time it will take to you to complete it. You can also only write 7 or 8 of them if you want, the exercise is not meant to be boring.

</div>

| Method | Requirements|
|---|---|
|**/Get**|Return a hello world message|
|**/DaysBetweenDates**|Calculate days between two dates. <br/>Receive by query string 2 parameters date1 and date 2 , and calcualte the days that are between those two dates.|
|**/Validatephonenumber**|Receive by querystring a parameter called `phoneNumber`. <br/>Validate `phoneNumber` with Spanish format, for example +34666777888<br/>if `phoneNumber` is valid return "valid"<br/>if `phoneNumber` is not valid return "invalid"|
|**/ValidateSpanishDNI**|Receive by querystring a parameter called `dni`. calculate DNI letter<br/>if DNI is valid return "valid"<br/>if DNI is not valid return "invalid"<br/>We will create automated tests to check that the functionality is correctly implemented.<br/>When the development is completed, we will build a container using Docker|
|**/ReturnColorCode**|Receive by querystring a parameter called `color`<br/>read `colors.json` file and return the `rgba` field<br/>get color var from querystring<br/>iterate for each color in colors.json to find the color<br/>return the code.hex field|
|**/TellMeAJoke**|Make a call to the joke api and return a random joke using axios|
|**/MoviesByDirector**|(this will require to browse to [https://www.omdbapi.com/apikey.aspx](https://www.omdbapi.com/apikey.aspx) and request a FREE API Key)<br/>Receive by querystring a parameter called director<br/>Make a call to the movie api and return a list of movies of that director using axios<br/>Return the full list of movies|
|**/ParseUrl**|Retrieves a parameter from querystring called someurl<br/>Parse the url and return the protocol, host, port, path, querystring and hash<br/>Return the parsed host|
|**/ListFiles**|Get the current directory<br/>Get the list of files in the current directory<br/>Return the list of files|
|**/GetFullTextFile**|Read `sample.txt` and return lines that contains the word "Fusce". (becareful with this implementation, since this normally reads the full content of the file before analizing it, so memory usage is high and may fail when files are too big)|
|**/GetLineByLinefromtTextFile**|Read `sample.txt` line by line<br/>Create a promise to read the file line by line, and return a list of lines that contains the word "Fusce"<br/>Return the list of lines|
|**/CalculateMemoryConsumption**|Return the memory consumption of the process in GB, rounded to 2 decimals|
|**/MakeZipFile**|Using zlib create a zip file called `sample.gz` that contains `sample.txt`|
|**/RandomEuropeanCountry**|Make an array of european countries and its ISO codes<br/>Return a random country from the array<br/>Return the country and its ISO code|

## GitHub Copilot Chat exercises

These tasks can be performed with the [GitHub Copilot Chat](https://marketplace.visualstudio.com/items?itemName=GitHub.copilot-chat) add-in.

- **Explain**

Select the line that has the regex in the validatePhoneNumber method, and use `/explain` comamand. You will see an explanation detailing what each different notation does in the regular expression.

- **Language translation**

Select some source code, like this line:

``` js
var randomCountry = countries[Math.floor(Math.random() * countries.length)];
```

Ask to the chat to translate it to another language, for example Python. You should see new code generated in **python**

- **Readable**

Select the content of MakeZipFile

Ask to the chat to make it more readable. See how comments are added and also variables that have short names are renamed to more understandable names.

- **Fix Bug**

In the exercise, there should be no bugs, since most of the code will be done by GitHub Copilot. We can force some errors and then test the debug functionality.

Force some errors like:

In a for loop change the beginning to (change the 0 for a 1):

``` js
    for (var i = 1
```

select the text and ask to the chat to fix the bug.

- **Make robust**

Select some text that comes from input, for example, variables that come from query string:

``` js
        var queryData = url.parse(req.url, true).query;
        var date1 = queryData.date1;
        var date2 = queryData.date2;
```

Ask to the chat to make it robust, and you will see that additional validation is added.

- **Document**

Select some line (e.g. a method or the beginning of the if clause)

``` js
    else if (req.url.startsWith('/GetFullTextFile')) 
```

Ask to the chat to document it. You will see that GitHub Copilot chat will explain what the code does and add comments to the code.

---

# Lab: .NET

The goal is to create a simple WebAPI using .NET 6.0 and Docker with the help of GitHub Copilot.
Follow the instructions below and try to use GitHub Copilot as much as possible.
Try different things and see what GitHub Copilot can do for you, like generating a Dockerfile or a class, adding comments, etc.

Remember:

Make sure GitHub Copilot is configured and enabled for the current language, just check the status bar on the bottom right corner of VS Code.

## Create dotnet WebAPI project

- Create a new NET project using

``` powershell
dotnet new webapi
```

- Create a new file `User.cs` in the Models folder, and instruct GitHub Copilot to generate a class for you.

- Add a new file `UserController.cs` in the Controllers folder that inherits from ControllerBase, and instruct GitHub Copilot to generate a controller for you.

- Add `ApiController` and Route attributes to the class.

- Add a new file `IUserService` in the Abstractions folder, and instruct GitHub Copilot to generate an interface for you.

- Run the app using (if you are working with GitHub Codespaces you may need to remove HTTPS redirection from `Program.cs` )

```  powershell
dotnet run
```

- Implement the interface IUserService in `UserService.cs` in the Services folder and add some comments so GitHub Copilot be able to generate the implementation for you.

- Instruct GitHub Copilot to generate a List for Users and the Add and Get Methods using the list.

- Go to `Program.cs` a inject the `IUserService` before building the app.

``` csharp
builder.Services.AddSingleton<IUserService, UserService>();
```

- Run the app using

``` powershell
dotnet run
```

> If you run into and "No server certificate was specified..." error, run the following command

``` powershell
dotnet dev-certs https
```

- Forward port if needed

- Navigate to your address /swagger. Example: [https://leomicheloni-supreme-space-invention-q74pg569452ggq-5164.preview.app.github.dev/swagger/index.html](https://leomicheloni-supreme-space-invention-q74pg569452ggq-5164.preview.app.github.dev/swagger/index.html)

## Put the application into a Docker container

- Publish the app and put it in a folder called _publish_

``` dotnet
dotnet publish -c Release -o publish
```

- Using the existing `Dockerfile`, put the app in a container and run it (add more instructions or start to write code and let GitHub Copilot complete it for you)
- Build the image and run the app on port 8080

``` powershell
docker build -t dotnetapp .
docker run -d -p 8080:80 --name dotnetapp dotnetapp
```
