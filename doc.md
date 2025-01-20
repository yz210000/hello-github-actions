Feature: 容灾主备站点间 Secret 信息同步

  Scenario: 建立产品容灾关系时 Secret 全量同步成功
    Given 未建立产品容灾关系
    When 建立产品容灾关系
    Then 主站点向备站点全量同步 Secret 成功
    Then 主站点与备站点 Secret （drSync=true） 内容相同
    Then 主站点的 DrSecretResource 状态变为 Active
    Then 备站点的 DrSecretResource 状态变为 Standby

  Scenario: 倒换时 Secret 同步成功
    Given 已建立产品容灾关系
    When 执行倒换
    Then 主站点向备站点全量同步 Secret 成功
    Then 主站点与备站点 Secret （drSync=true） 内容相同
    Then 主站点的 DrSecretResource 状态变为 Active
    Then 备站点的 DrSecretResource 状态变为 Standby

  Scenario: 删除产品容灾关系时 Secret 停止同步成功
    Given 已建立产品容灾关系
    When 执行删除产品容灾关系
    Then 所有站点停止同步 Secret
    Then 主站点的 DrSecretResource 状态变为 Nodr
    Then 备战点的 DrSecretResource 状态变为 Nodr
