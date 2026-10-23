# A step-by-step guide for storing an API key in the CLI and then retrieving it in a Python notebook

## For both **Mac** (using Terminal) and **Windows** (using Command Prompt or PowerShell):

### Part 1: Storing an API Key using CLI

#### Mac (Terminal) and Windows (Command Prompt/PowerShell)

##### 1. **Choose the environment variable name:**
   - Before storing the key, decide on a descriptive environment variable name, e.g., `MY_API_KEY`.

##### 2. **Set the environment variable in CLI:**

- **Mac (using Terminal):**

  You can store the key in your environment variables using the `export` command:

  ```bash
  export MY_API_KEY='your_api_key_here'
  ```

  This will store the API key for the current Terminal session.

- **Windows (using Command Prompt):**

  To store the key for the current Command Prompt session, use the `set` command:

  ```cmd
  set MY_API_KEY=your_api_key_here
  ```

- **Windows (using PowerShell):**

  To store the key in PowerShell for the current session, use the `Set-Item` command:

  ```powershell
  $env:MY_API_KEY='your_api_key_here'
  ```

##### 3. **Make the environment variable permanent (optional):**

   If you want the environment variable to persist across sessions (so you don't have to set it every time):

- **Mac:**

  Edit your shell profile (`.bash_profile`, `.bashrc`, or `.zshrc` depending on the shell you're using):

  ```bash
  nano ~/.bash_profile
  ```

  Then, add the following line:

  ```bash
  export MY_API_KEY='your_api_key_here'
  ```

  After saving, run this command to apply the changes immediately:

  ```bash
  source ~/.bash_profile
  ```

- **Windows:**

  You can use the `setx` command to make it permanent for future sessions:

  ```cmd
  setx MY_API_KEY "your_api_key_here"
  ```

  Note: This will not affect the current session; it will only apply to new Command Prompt windows.

### Part 2: Retrieving the API Key in a Python Notebook

Once the API key is stored as an environment variable, you can access it in a Python notebook using the `os` module.

#### 1. **Import the `os` module in your notebook:**

   Open your Python notebook and start by importing the `os` module:

   ```python
   import os
   ```

#### 2. **Retrieve the API key from the environment variable:**

   Use the `os.getenv()` method to get the stored API key:

   ```python
   api_key = os.getenv('MY_API_KEY')
   ```

   Now, `api_key` will hold the value of your API key.

#### 3. **Use the API key in your code:**

   You can now use the `api_key` variable in your code where the API key is required:

   ```python
   if api_key:
       print("API Key retrieved successfully!")
   else:
       print("API Key not found!")
   ```

#### 4. **Error Handling (Optional):**

   To handle the case where the environment variable might not be set, you can provide a default value or raise an error if the key is missing:

   ```python
   api_key = os.getenv('MY_API_KEY', 'default_value_if_not_set')

   if api_key == 'default_value_if_not_set':
       raise ValueError("API Key not found in environment variables!")
   ```

### Summary of Commands

| Step                     | Mac (Terminal)                              | Windows (Command Prompt)              | Windows (PowerShell) |
|--------------------------|---------------------------------------------|---------------------------------------|----------------------|
| Set environment variable  | `export MY_API_KEY='your_api_key_here'`     | `set MY_API_KEY=your_api_key_here`    | `$env:MY_API_KEY='your_api_key_here'` |
| Make variable permanent   | Add `export` command to `.bash_profile`     | `setx MY_API_KEY "your_api_key_here"` | (same as Command Prompt) |
| Access variable in Python | `os.getenv('MY_API_KEY')`                   | `os.getenv('MY_API_KEY')`             | `os.getenv('MY_API_KEY')` |

This guide will work for locally running Python notebooks in both Mac and Windows environments. If you follow these steps, your API key will be safely stored and accessible within your notebook whenever you need it.

## Storing API Keys using VSC Terminal and notebook server

After restarting your `gdal-env` Conda environment, you can test that the environment variable has been correctly stored by checking it in the terminal. Here's how you can verify that the variable is stored and accessible after restarting the environment:

### Step-by-Step Guide to Testing the Environment Variable in the Terminal

#### Step 1: Restart the Terminal and Activate the Conda Environment

1. **Open the VS Code Terminal** (or a new terminal window outside VS Code if preferred).
2. **Activate your `gdal-env` environment** by running:

   ```bash
   conda activate gdal-env
   ```

#### Step 2: Check if the Environment Variable is Set

Once the environment is activated, you can test whether the variable is stored by echoing it:

1. Run the following command to display the value of the environment variable:

   ```bash
   echo $MY_API_KEY
   ```

   - If the environment variable is set correctly, you will see the value of `MY_API_KEY` printed in the terminal.
   - If the environment variable is not set or accessible, nothing will be printed or you'll see an empty line.

#### Step 3: Debugging

If you don't see the value of `MY_API_KEY` printed:

- **Ensure the environment variable was correctly set for the Conda environment** by checking the environment variables configured for your Conda environment:

   ```bash
   conda env config vars list
   ```

   This will list all the environment variables stored for the active environment (`gdal-env`). Check if `MY_API_KEY` is in the list.

- **If `MY_API_KEY` is not in the list**, you may need to re-run the following command to store it persistently:

   ```bash
   conda env config vars set MY_API_KEY='your_api_key_here'
   ```

   Then deactivate and reactivate the environment:

   ```bash
   conda deactivate
   conda activate gdal-env
   ```

   After reactivating the environment, run `echo $MY_API_KEY` again to verify it’s set.

### Summary of Commands:

- **Activate Conda environment:**

   ```bash
   conda activate gdal-env
   ```

- **Check the environment variable:**

   ```bash
   echo $MY_API_KEY
   ```

- **List configured environment variables for the Conda environment:**

   ```bash
   conda env config vars list
   ```

By following these steps, you can test whether the environment variable is correctly stored and accessible from the terminal after restarting your Conda environment.
