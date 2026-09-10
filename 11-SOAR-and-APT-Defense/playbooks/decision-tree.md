# Automation Decision Tree - Suspicious Authentication

Suspicious Authentication
    |
    v
Is source unusual?
    No -> Monitor
    Yes -> Enrich (threat intelligence lookup)
               |
               v
        Related activity found?
            No -> Monitor
            Yes -> High Risk
                      |
                      v
                Human Review
                    |
            +-------+-------+
            |               |
        Approve          Reject
            |               |
            v               v
      Containment       Continue Investigation
