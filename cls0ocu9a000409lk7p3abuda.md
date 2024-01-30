---
title: "VSCode Bridge to (EKS) kubernetes"
datePublished: Tue Jan 30 2024 18:11:01 GMT+0000 (Coordinated Universal Time)
cuid: cls0ocu9a000409lk7p3abuda
slug: vscode-bridge-to-eks-kubernetes
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/vk0zqWdpGLk/upload/b6b17ea3d3798870491a5a68df0920bb.jpeg
tags: kubernetes, k8s, vscode-cjevho8kk00bo1ss2lmqqjr51, vscode-extensions, bridge

---

Getting [bridge to kubernetes to work](https://learn.microsoft.com/en-us/visualstudio/bridge/overview-bridge-to-kubernetes) with AWS's EKS needs some fussin'.

If you are authorized via SSO, managed by [aws-vault](https://github.com/99designs/aws-vault) this should help.

You need to have the `aws-vault exec <profile>` loaded before running `k-creds`. Relevant AWS environment variables are written to `~/.envs_temp` which is rigged to be automatically loaded in new (ZSH) shells' that will be available to VSCode.

You should now be able to see nodes in your cluster.

```bash
function k-creds () {                                                                                                                                                            
    RC_FILE="${RC_FILE:-~/.zshrc}"                                                                                                                                                
    DEV_PROFILE="${DEV_PROFILE:-dev-profile}"                                                                                                                             
   
    # load                                                                                                                                                                           
    grep -q envs_temp $RC_FILE || (echo "[ -f ~/.envs_temp ] && source ~/.envs_temp" >> $RC_FILE; echo "Updated $RC_FILE")
    aws-vault export $DEV_PROFILE | sed 's/^/export /' > ~/.envs_temp && echo "Got AWS '$DEV_PROFILE' credentials, please restart vs-code"                                     
}
```