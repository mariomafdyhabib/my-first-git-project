Git commands: git add . , git commit -am "" , git push , git status , git log --oneline ,  git diff 5c3de53~1 5c3de53 calculator.py , git stash
git revert 5c3de53 , git stash pop

git log --oneline
af86521 (HEAD -> main) feat: Add divide function with zero check
5c3de53 fix: Optimize subtract function logic (introducing bug)
fd12e09 feat: Add multiply function
8dd8cf0 feat: Add basic calculator functions (add, subtract)
d61e81e (origin/main) Clean
--------
1- Explain in your deliverables: What does this git diff command show you? How did it help you confirm the bug?

git diff 5c3de53~1 5c3de53 calculator.py
diff --git a/calculator.py b/calculator.py
index d9c5fe0..0119279 100644
--- a/calculator.py
+++ b/calculator.py
@@ -3,9 +3,9 @@ def add(a, b):
     return a + b
 
 def subtract(a, b):
-    return a - b
+    # THIS IS THE BUG! Should be 'a - b'
+    return a + b # Intentional bug: changed to addition!
 
[This diff confirms the bug by showing that:

The correct subtraction logic (a - b) was replaced with incorrect addition logic (a + b).]
-------

2- Explain in your deliverables: Why is git stash useful in this scenario?

Saved working directory and index state WIP on main: af86521 feat: Add divide function with zero check

[git stash is useful here because it:

Prevents loss of in-progress work
Enables safe context-switching to investigate bugs
Helps keep the commit history clean by avoiding unnecessary "work-in-progress" commits]
--------

3- Fix the Erroneous Commit (Choose ONE method and justify):

Option B: git revert 5c3de53

[git revert was the best choice here because the buggy commit was already pushed to a shared branch.
It safely created a commit that reversed the buggy code, while preserving collaboration and history.
git reset would have risked disrupting other developers’ work and is not appropriate in this case.
]

Why not git reset --hard in this case?

Rewrites commit history, which is unsafe for shared branches
If already pushed, teammates' histories will diverge, causing major conflicts
Requires force-push (git push --force), which can accidentally delete others' work
-----------

4- Explain in your deliverables: What is the difference between git stash pop and git stash apply? Why did you choose pop (or apply)?

| Command           | What it does                                                           |
| ----------------- | ---------------------------------------------------------------------- |
| `git stash apply` | Reapplies the stashed changes **but keeps them in the stash list**     |
| `git stash pop`   | Reapplies the stashed changes **and removes them from the stash list** |

Why did I choose git stash pop?
I chose git stash pop because:

I was ready to resume working on the changes I stashed.
I no longer needed to keep the stash entry—restoring it once was enough.
It helped me keep the stash list clean and avoid clutter from unused entries.
