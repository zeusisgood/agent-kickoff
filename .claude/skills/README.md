# 同梱のスキル

外部のリポから写したスキル（rules-adr 0018）。元の LICENSE を各ディレクトリに置く。

| スキル | 元のリポ | 写したコミット | ライセンス | 写したあとの変更 |
|---|---|---|---|---|
| `security-audit` | [cloudflare/security-audit-skill](https://github.com/cloudflare/security-audit-skill) の `skills/security-audit/` | `c1c8a8c1471069fb0e188eeaff69b8e8db6564a8` | MIT | なし |
| `ponytail` | [DietrichGebert/ponytail](https://github.com/DietrichGebert/ponytail) の `skills/ponytail/` | `09c434ab73ca43761c5d8b0c5d341926c2fba710` | MIT | frontmatter に `disable-model-invocation: true` |
| `ponytail-audit` | 同上の `skills/ponytail-audit/` | 同上 | MIT | 同上 |
| `ponytail-review` | 同上の `skills/ponytail-review/` | 同上 | MIT | 同上 |

- ponytail の 3 つは、ユーザーが `/ponytail`・`/ponytail-audit`・`/ponytail-review` と打ったときだけ動く。
- 更新を取り込むときは、元のリポの差分を読んでから写し直し、この表のコミットを書き換える。
