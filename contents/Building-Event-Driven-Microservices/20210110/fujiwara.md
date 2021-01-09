## 読書会当日に話したいこと

- Customer全員とJoint Meetingする？何を以てProspectiveなConsumerとするか？
    - Event DesignにおいてProspectiveなConsumerとMeetingをして設計をすべきという趣旨は理解するものの、
    具体的な基準が無い。「1.将来の/予想される」という意味と「2.有望な/見込みのある」という意味があると思いますが、
    皆さんは、1だとしたら都度Joint Meetingをしっかりする？その場合に話すべき項目は？
      - their own needs and anticipated business functions
    2.だとすると、どんなCustomerがProspectiveだと思いますか？

## 読書メモ

# Chapter3
- data contract
    - data definition
    - triggering logic
- WARNING
    - It may be tempting to build a common library that interprets any given event for all services, but this creates problems with multiple language formats, event evolutions, and independent release cycles. Duplicating efforts across services to ensure a consistent view of implicitly defined data is nontrivial and best avoided completely.
- Schema Definition Comments
  - Specifying the triggering logic of the event. This is typically done in a block header at the top of the schema definition and should clearly state why an event has been generated.
  - Giving context and clarity about a particular field within the structured schema. For example, a datetime field’s comments could specify if the format is UTC, ISO, or Unix time.
- Full-Featured Schema Evolution
- Involve Prospective Consumers in the Event Design
    - ProspectiveなConsumerの見分け方は？
# Chapter4
- Data liberation
- change-data capture (CDC)
