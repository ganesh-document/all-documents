# **GitHub Docs**

1. **Get started**
2. **Collaborative coding**
3. **CI/CD and DevOps**
4. **Security**
5. **Client apps**
6. **Project management**
7. **Developers**
8. **Enterprise and Teams**
9. **Community**


https://docs.github.com/en


     run: |
       chmod +x ./update_git_doc.sh
       ./update_git_doc.sh ${{ env.GA_SECRET }}
      shell: bash


curl -L \
  -X POST \
  -H "Accept: application/vnd.github+json" \
  -H "Authorization: Bearer xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"\
  -H "X-GitHub-Api-Version: 2022-11-28" \
  https://api.github.com/orgs/ganesh-document/repos \
  -d '{"name":"Hello-World","description":"This is your first repository","homepage":"https://github.com","private":false,"has_issues":true,"has_projects":true,"auto_init":true}'


curl -L \
  -X DELETE \
  -H "Accept: application/vnd.github+json" \
  -H "Authorization: Bearer xxxxxxxxxxxxxxxxxxxxxx"\
  -H "X-GitHub-Api-Version: 2022-11-28" \
  https://api.github.com/repos/ganesh-document/Hello-World


curl -L \
  -X PUT \
  -H "Accept: application/vnd.github+json" \
  -H "Authorization: Bearer xxxxxxxxxxxxxxxxxxxxxx"\
  -H "X-GitHub-Api-Version: 2022-11-28" \
  https://api.github.com/repos/ganesh-document/Hello-World/branches/master/protection \
  -d '{"required_status_checks":{"strict":true,"contexts":["continuous-integration/travis-ci"]},"enforce_admins":true,"required_pull_request_reviews":{"dismissal_restrictions":{"users":["octocat"],"teams":["justice-league"]},"dismiss_stale_reviews":true,"require_code_owner_reviews":true,"required_approving_review_count":2,"require_last_push_approval":true,"bypass_pull_request_allowances":{"users":["octocat"],"teams":["justice-league"]}},"restrictions":{"users":["octocat"],"teams":["justice-league"],"apps":["super-ci"]},"required_linear_history":true,"allow_force_pushes":true,"allow_deletions":true,"block_creations":true,"required_conversation_resolution":true,"lock_branch":true,"allow_fork_syncing":true}'












curl -L \
  -X POST \
  -H "Accept: application/vnd.github+json" \
  -H "Authorization: Bearer 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"\
  -H "X-GitHub-Api-Version: 2022-11-28" \
  https://api.github.com/repos/ganesh-document/Hello-World/rulesets \
  -d '{"name":"super cool ruleset","target":"branch","enforcement":"active","bypass_mode":"repository","bypass_actors":[{"actor_id":234,"actor_type":"Team"}],"conditions":{"ref_name":{"include":["refs/heads/main","refs/heads/master"],"exclude":["refs/heads/dev*"]}},"rules":[{"type":"commit_author_email_pattern","parameters":{"operator":"contains","pattern":"github"}}]}, "rules":[{"type":"pull_request","parameters":{"required_approving_review_count":"1"}}]}, "rules":[{"type":"non_fast_forward","parameters":{"type":"non_fast_forward"}}]}'


