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