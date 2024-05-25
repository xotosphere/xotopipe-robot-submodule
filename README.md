# xotopipe action submodules

### summary

When working with a repository that has multiple submodules, it can be difficult to keep track of changes and pipelines across all submodules. 

This can lead to inefficiencies and errors in the development process. To address this problem, we have created a custom GitHub action that automatically creates a bot comment in the root pull request, listing all pull requests of submodules, including their status and pipeline.

### description

To use this action, follow these steps:

1. Add a job with this action in your workflow file:

```yaml
custom-action:
  runs-on: ubuntu-latest
  container:
    image: node:16
    options: --user root
  steps:
    - name: Checkout root repo
      uses: actions/checkout@v3
      with:
        repository: xotosphere/xotopipe-robot-submodule
        token: ${{ secrets.GH_PAT }}
    - name: Sync submodules changelog
      uses: ./
      with:
        github_token: ${{ secrets.GITHUB_TOKEN }}
        xotocross_github_access_token: ${{ secrets.GH_PAT }}
        owner: xotopipe
        submodules: |
          submodule-1
          submodule-2
        branch: ${{ github.head_ref || github.ref_name }}
        workflow: ci-workflow.yml
```

2. In the job, specify the required inputs:
- **`github_token`**: a GitHub token for the CI.
- **`xotocross_github_access_token`**: a personal access token with the **`repo`** scope to access all repos of the organization.
- **`owner`**: the organization (xotoscript).
- **`submodules`**: a list of submodules in the repository.
- **`branch`**: the name of the branch of the current pull request.
- **`workflow`**: the name of the workflow file to use.
3. Run the workflow.

The action will automatically create a bot comment in the root pull request, listing all pull requests of submodules, including their status and pipeline.

### conclusion

With our custom GitHub action, you can easily keep track of changes and pipelines across all submodules in your repository, reducing inefficiencies and errors in the development process. Use this action in your workflow to improve your development process today.
