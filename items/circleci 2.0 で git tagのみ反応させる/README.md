# TL;DR

tagでも前のworkflowsが動くようにする必要がある。

# 1.0のとき

deploymentに書くだけで動いたのにどうして。

# document(2017-12-31時点)

https://circleci.com/docs/2.0/workflows/#git-tag-job-execution

> CircleCI treats tag and branch filters differently when deciding whether a job should run.
> 1. For a branch push unaffected by any filters, CircleCI runs the job.
> 2. For a tag push unaffected by any filters, CircleCI skips the job.

サポートフォーラムに書く寸前まで来て、何度も読み返してたら気づいた。
つまり、これじゃ前の依存が起動しないからダメ

```yaml
workflows:
  version: 2
  build_and_deploy:
    jobs:
      - build
      - package:
          requires:
            - build
      - deploy:
          requires:
            - package
          filters:
            tags:
              only: /.*/
            branches:
              ignore: /.*/
```

セイカイ

```yaml
workflows:
  version: 2
  build_and_deploy:
    jobs:
      - build:
          filters:
            tags:
              only: /.*/
      - package:
          requires:
            - build
          filters:
            tags:
              only: /.*/
      - deploy:
          requires:
            - package
          filters:
            tags:
              only: /.*/
            branches:
              ignore: /.*/
```

わかるかあああああ
