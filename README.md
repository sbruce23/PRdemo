# PRdemo
Repo for students to practice creating a pull request after forking a repo

1. First, make a fork of the GitHub repo.

    a. Visit URL: [https://github.com/haseungyeon3/PRdemo/](https://github.com/haseungyeon3/PRdemo/)

    b. In the top right corner of the screen, click on the down arrow next to "Fork" and select "Create a new fork." This creates an independent copy of the GitHub repo, which is then saved as a repository under your GitHub account.

    *Note that if you are already listed as a collaborator on the repo, or it is your own repo, you can skip this step in practice.

2. Clone the forked GitHub repository from your GitHub account (`git clone https://github.com/your-username/PRdemo.git`), replacing `your-username` with your actual GitHub username.

3. In a terminal window located at the folder, run:

    a. `git checkout main` (make sure you are on the main branch)
    
    b. `git branch dev` (create the new branch)
    
    c. `git checkout dev` (checkout the new branch)

4. Edit `sleephour.xlsx` on your local machine in the directory by adding your daily sleep hours to the file and save it.

5. In the terminal window run:

    a. `git status` (should show that `sleephour.xlsx` has been modified but is not in the staging area)
    
    b. `git add .` (Should add `sleephour.xlsx` to the staging area; run `git status` if you want to confirm this)
    
    c. `git commit -m 'added daily sleep hour <insert name here>' ` replacing `<insert name here>` with yours
    
    d. `git push --set-upstream origin dev` (set up and use a classic security token if needed to be able to do this)

6. Create a pull request on GitHub to merge your changes from your forked repository into the original repository:

    a. Navigate to your forked repository on GitHub by going to the URL: [https://github.com/your-username/PRdemo](https://github.com/your-username/PRdemo), replacing `your-username` with your actual GitHub username.

    b. At the top of your repository, locate and click on the "Pull Requests" tab.

    c. Click the green "New Pull Request" button.

    d. On the "Compare changes" page, ensure that the "base repository" is set to `sbruce23/PRdemo` and the "base" branch is set to `main`.

    e. In the "head repository" drop-down, select your forked repository.

    f. Choose the `dev` branch (or the branch where you made your changes) as the "compare" branch.

    g. Review the changes and ensure that they are as you intended.

    h. If everything looks good, click the "Create Pull Request" button.

    i. Give your pull request a meaningful title and description. Describe the changes you made and why they are necessary.

    j. Once you're satisfied with your description, click the "Create Pull Request" button again.

    k. Your pull request will now be visible in the original repository's pull requests. Other collaborators can review your changes, provide feedback, and discuss any potential modifications.

    l. If there are no conflicts and your changes are approved, the repository owner or collaborators can merge your pull request by clicking the "Merge Pull Request" button.

    m. Congratulations, your changes are now part of the original repository!
