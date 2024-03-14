



##  - Code Scanning AI


**Scenario**

You have just joined a new team as a developer. To familiarize yourself with the codebase, you've been tasked with remediating some code scanning vulnerabilities in the repository.

You will be remediating an existing SQL Injection vulnerability in `main.go` on **line 309**.
There are two tasks to remediate this vulnerability:
1. sanitize input in the javascript (Exercise 1)
2. fix the SQL prepare statement in the go code (Exercise 2 and Exercise 3)

### Exercise 1 - AI generated autofix on javascript pull requests - 10 mins

This Universe we will be launching the **code scanning autofix** feature as a limited public beta. This feature uses AI to generate fixes on pull requests that contain JavaScript CodeQL alerts.  We will see this feature in action in this exercise. If you are interested in participating in this limited public beta, please reach out to your Account Manager if you are an existing customer. Otherwise, reach out to the GitHub Sales Team for assistance. You can find the terms and conditions [here](https://docs.github.com/en/site-policy/github-terms/github-terms-for-additional-products-and-features).

Input sanitization is a fundamental security practice to prevent SQL injection attacks. Let's add a sanitize method in the javascript to help in mitigating against injection attack vectors.

You can solve this exercise using either the codespaces or the UI. Codespaces is preferable as this is what a developer would use under normal circumstances. However, if codespaces is not loading for you please use the UI. 


1. Create a branch called `sql-injection-fix` and push it to the remote repo.

    <details>
      <summary> Hint </summary>
      Run the command:
        
      ```
        $ git checkout -b sql-injection-fix
        $ git push -u origin sql-injection-fix
      ```
     </details>

    <details>
      <summary> Solution </summary>  
        
      ![create-branch](https://github.com/octodemo/universe-wip/assets/68650974/4a162cb4-62d7-4ce6-9114-c5efefe60b2d)
  
    </details>
     

2. Add the following sanitization function on **line 233** of `frontend/components/Gallery.vue`

    ```js
    function sanitizeInput(input) {
        if (input == null) {
            return "";
        }
        //escape all occurances of apostrophe
        input = input.replace("'", "''");
    
        return input;
    }
    ```

3. Call the sanization function from the Update function by placing the following call on **line 347** of `/frontend/components/Gallery.vue`

    ```js
        artItem.description = sanitizeInput(artItem.description)
        artItem.title = sanitizeInput(artItem.title)
    ```

4. Commit and push the code

<details>
   <summary> Solution for steps 2-4 </summary>  
    
   ![sanitization](https://github.com/octodemo/universe-wip/assets/68650974/a85a6690-607d-467e-b6bf-3566ad73d5b9)
   
</details>

5. Raise a pull request to the `main` branch. Wait for the scans to complete and you should see a CodeQL javascript alert in your pull request. Oh no! There is a vulnerability in our vulnerability! Lucky we have autofix.


