# Frappe 官方镜像同步仓库

![GitHub Workflow Status](https://img.shields.io/github/actions/workflow/status/wolono/sync/sync-frappe.yml?label=镜像同步)

本仓库通过GitHub Actions实现Frappe系列官方仓库的定时镜像同步，确保AtomGit等国内镜像仓库与GitHub官方仓库保持更新同步。

## 主要功能

✅ **自动化同步**  
- 每日UTC时间00:00自动触发同步（北京时间08:00）
- 支持手动触发即时同步

🔄 **支持同步的仓库**  
| 仓库名称   | GitHub官方仓库                      | 国内镜像地址                        |
|------------|-----------------------------------|-----------------------------------|
| frappe     | <https://github.com/frappe/frappe.git> | <https://atomgit.com/frappe/frappe.git> |
| erpnext    | <https://github.com/frappe/erpnext.git> | <https://atomgit.com/frappe/erpnext.git> |
| hrms       | <https://github.com/frappe/hrms.git>    | <https://atomgit.com/frappe/hrms.git>    |
| crm        | <https://github.com/frappe/crm.git>     | <https://atomgit.com/frappe/crm.git>     |
| wiki       | <https://github.com/frappe/wiki.git>    | <https://atomgit.com/frappe/wiki.git>    |
| insights   | <https://github.com/frappe/insights.git> | <https://atomgit.com/frappe/insights.git> |

## 工作机制

1. **镜像克隆**：使用`git clone --mirror`完整克隆仓库
2. **认证配置**：通过GitHub Secrets注入AtomGit账号凭据
3. **强制同步**：使用`git push --force --mirror`覆盖式同步
4. **错误重试**：失败时自动重试2次，间隔10秒

# Frappecn 镜像同步

本项目用于自动同步 Frappecn 相关仓库至 AtomGit 镜像，使用 GitHub Actions 实现定时与手动触发。

## 工作流说明

- 工作流文件：`.github/workflows/sync-frappecn.yml`
- 功能：定时（每天零点）或手动同步以下仓库的主仓库与 AtomGit 镜像仓库。
- 当前同步仓库列表：
  - frappecn/frappe
  - frappecn/erpnext
  - frappecn/hrms
  - frappecn/crm
  - frappecn/bench

## 使用方法

1. 配置仓库 Secrets：
   - `ATOMGIT_USERNAME`：AtomGit 用户名
   - `ATOMGIT_TOKEN`：AtomGit 访问 Token

2. 工作流会自动比对上游与下游仓库的最新提交，如已同步则跳过，否则强制推送所有分支与标签。

3. 支持重试机制，最多重试 2 次。

## 注意事项

- 仅同步主分支及所有标签，不包含 notes 引用。
- 推送后自动清理临时目录。