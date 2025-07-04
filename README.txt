Getting Started: Gemini CLI ↔ Google AI Studio Workflow
Below is a step-by-step guide to kick off your AI-driven development loop. 
You’ll use Gemini CLI to read your markdown docs, generate AI prompts, feed them to Google AI Studio, 
retrieve the code it spits out, then have Gemini validate and update your task files before moving on.

1. Configure Gemini CLI
------------------------
1. Install Gemini CLI (adjust to your environment): (Bash)
npm install -g @your-org/gemini-cli

2. In your project root, create a gemini.config.json: (json)
{
  "memoryBank": "AITaskDocs/ProjectOverview.md",
  "tasksDir":    "AITaskDocs",
  "outputDir":   "generated-code"
}

3. Verify config: (Bash)
gemini-cli doctor


2. Generate Your First Prompt
------------------------------
1. Ask Gemini to read the ProjectOverview and your first task: (Bash)
gemini-cli prompt --task AITaskDocs/Task01_Setup.md --out prompts/Task01.txt


2. Inspect prompts/Task01.txt. This contains the AI-friendly specification.


3. Run the Prompt in Google AI Studio
--------------------------------------
- Open Google AI Studio and create a new “Text to Code” job.
- Copy the contents of prompts/Task01.txt into the prompt field.
- At the beginning of the prompt, add the line "use context7" to leverage up-to-date documentation.
- Configure the job (language: TypeScript/JavaScript, Next.js target).
- Run and download the resulting code bundle to:
generated-code/Task01_Setup/


4. Ingest Generated Code Back into Gemini
------------------------------------------
1. Hand off the new code to Gemini for validation and to update your task markdown: (Bash)
gemini-cli ingest --task AITaskDocs/Task01_Setup.md --codeDir generated-code/Task01_Setup

2. Gemini will:
- Run your tests/linting
- Update Task01_Setup.md fields (Last Stopped, % Complete, next steps)

4b. Run the Generated Code Locally
Once the code is ingested and validated, you’ll want to run it to see the results in your browser.

1. Navigate to the generated code directory: (Bash)
cd generated-code/Task01_Setup

2. Install dependencies. If the generated code includes a package.json file: (Bash)
npm install

3. Start the development server for a Next.js project: (Bash)
npm run dev

4c. Troubleshooting & Environment Setup
If the code references environment variables (e.g., database URL, API keys), create a .env.local file in the root of the generated code directory and populate it with the required values.
If Prisma is used, run: (Bash)
npx prisma generate
npx prisma migrate dev

4d. View the App in Your Browser
Once the dev server is running, open your browser and go to: http://localhost:3000




5. Check Progress & Move to Next Task
--------------------------------------
1. View overall status: (Bash)
gemini-cli status

You’ll see which task is next and high-level progress.

2. Kick off the next task (Task02) just like you did for Task01: (Bash)
gemini-cli prompt --task AITaskDocs/Task02_Auth.md --out prompts/Task02.txt

3. Repeat Steps 3–5 for every task until 100% complete.


6. Quick Reference of Commands
-------------------------------
gemini-cli prompt --task <task-md> --out <prompt-txt> (Generate an AI prompt from a task doc.)
gemini-cli ingest --task <task-md> --codeDir <dir> (Validate and merge AI-generated code; updates the task doc.)
gemini-cli status (See which task you’re on and overall completion.)
gemini-cli doctor (Verify your config and environment.)


7. Tips for Smooth Iteration
-----------------------------
- Keep your generated code in the generated-code/ sub-folders per task.
- After each ingest, commit your updated markdown and new code to Git.
- If you ever need to rerun a task (e.g., tests fail), use: (Bash)
gemini-cli reset --task AITaskDocs/Task01_Setup.md
- For design mocks, export Gemini’s prompt to Google Stitch AI—but treat it as a separate, parallel loop.

------------------------------------------------------------------------------------------------------------
Now you’re all set! Follow this loop for Tasks 01 through 08, and Gemini CLI plus Google AI Studio 
will orchestrate your entire dev lifecycle—no context lost, no manual bookkeeping.











