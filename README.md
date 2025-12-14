# Setup
mkdir git_assignment_HeroVired
cd git_assignment_HeroVired
git init

# Create calculator.py (paste initial content), then:
git add calculator.py
git commit -m "Initial commit: Calculator app skeleton"

# Dev branch and sqrt feature
git checkout -b dev
# Edit calculator.py to add square_root and enable test
git add calculator.py
git commit -m "Add square_root feature and test"

# Push and release v1
git remote add origin https://github.com/<your-username>/git_assignment_HeroVired.git
git push -u origin dev
git checkout main
git merge dev
git push -u origin main
git tag v1.0
git push origin v1.0

# Feature branch
git checkout dev
git checkout -b feature/sqrt
git commit -am "Refine square_root implementation (feature branch)"
git push -u origin feature/sqrt

# Bug fix on dev
git checkout dev
# Edit divide to prevent divide-by-zero
git commit -am "Fix: division by zero raises ValueError"
git push

# Keep feature/sqrt updated
git checkout feature/sqrt
git merge dev
git commit -m "Merge dev into feature/sqrt to include divide fix" || echo "No conflicts"
git push

# After PR approval
git checkout dev
git merge feature/sqrt
git push

# Final testing and v2 release
python calculator.py
git checkout main
git merge dev
git push
git tag v2.0
git push origin v2.0
