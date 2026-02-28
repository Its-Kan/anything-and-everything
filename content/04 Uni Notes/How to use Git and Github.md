---
share_link: https://share.note.sx/1w1vpjk5#HQcorHEnsCQwIz/FDK/jwDxyMTIBIOuDK2YoimKMWaE
share_updated: 2026-02-09T16:05:26+00:00
---
1. Download [Git](https://git-scm.com/downloads) and make a GitHub account, and install the GitLens extension 
	- *Git* tracks edits to code over time 
	- *GitHub* stores the master branch of code
	- *GitLens* helps us track the history of our edits

2. In Visual Studio Code, clone [this repository](https://github.com/UoY-Dylan/Y2S1-Music-Tech-Project/), and setup Git
	- This repository (called the *remote repository*) holds the main/master branch, and is where the most up-to-date code will be stored.
	- In the terminal, run these commands:
		- ``git config --global user.email "you@example.com"``
		- `git config --global user.name "John Doe"`

3. Create your own branch by clicking where it says **main** or **master** on the left of the bottom bar, and name it whatever you're working on.
	- For the sake of consistency, name it something like *feature/MenuSelect* or *fix/CrankAcceleration*
	- Making your own branch isolates any changes you make, which we can later merge into the main branch. This allows multiple of us to work on the same code.
	- Make a new branch for every new addition, fix, etc. you work on.
	- **Never** work on the master/main branch. It's reserved for code that's confirmed to work.

4. Write whatever code you need

5.  Stage your changes. Go to the **Source Control Panel** on the left, or by using $Ctrl+Shft+G$, and press the **+** icon to stage the files you've edited.
	- *Staging* means that the files are ready to be committed to the repository. 

6. Commit your changes. Again in the **Source Control Panel**, type a descriptive message of what you did, and click *Commit Changes*. You may need to click *Sync Changes* to push it to GitHub.
	- *Committing* means you're publishing your changes to the branch you're working on.

8. Go on GitHub and go to the *remote repository*. Once you think your code is ready, submit a *Pull Request*, to merge it with the master branch. 
	 - This prevents conflicts between different code coming in when we merge it to the master branch
	 - Once people have checked over the code and approve, I (Dylan) can merge it with the master branch.

9. Repeat from Step 3!

## Notes:
- It's better to commit with small, incremental changes rather than large ones. This means if we need to revert to an old version, we can do so easily.
- If you want to experiment with some new code, or work on a new branch *without publishing your changes by committing*, you can **stash** it, work on something new, then **apply** it if you're happy with it.
- If you need to update your branch with the latest commit in the main branch, **pull** it from the **Source Control Panel**.
