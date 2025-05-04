# MHEDAS_ML

## 👩‍💻 For Developers

### 🧠 Philosophy

**Branch boldly!**  
Have a new idea? Create a branch. Want to test something out? Create a branch.  
Don't overthink names — just do your best to describe what you’re working on.

---

### 🌳 Branching Guidelines

- Name your branch by purpose:  
  `new_section/feature_importance`, `bug_fix/bad_naming`, `update/data_cleaning`, etc.

If you are gonna add a SHAP plot today, for example, 
create a branch named new_section/shap_stuff 

Dont worry about disrupting anyones work, since you will be working on team_notebooks/ in your own. It does not matter if the notebooks are similar. 



> **Note from Daniel:**  
> My first branch's purpose is this README, so I created a branch named `update/git_guidelines`.  
> I will push it and make a pull request.

- Create as many branches as you want. Small is good!
- Don’t work directly on `main`.

---

### 🔄 Before You Start

Always make sure you're up to date:

```bash
git checkout main
git pull origin main
```

Try doing this everytime! You want to add another piece of work

Then create your branch

```bash
git checkout -b new_section/your_branch_name
```

Use VScode extension for github as much as possible to describe your commits, push, and pull request.

