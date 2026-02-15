# Network Troubleshooting Methodology 

A sturctured approach to diagnosing, resolving, and documenting network issures using tools like the OSI Model and industry best practices.
By using a sturctured approach I can increase the level of success, improve efficency, and prevent other issues going over looked.

---

## 5-Step Troubleshooting Process

```mermaid
flowchart TD
  start(Start) --> A

  subgraph Investigation & Diagnosing 
    A["1.Identify Problem"] --> B["2.Gather Information"]
    B --> C[["2a. Gather additional context<br/>(recent changes, user actions,<br/> error messages, changes in<br/>environment etc.)"]]
    C --> D[[2b. Analyze the problem<br/>with the information and<br/>eliminate possible common<br/>problems]]
  end;

  subgraph Diagnosis & Theory Testing
    D --> E{{"3. Establish a theory<br/>using the OSI Model"}}
    E --> F[["3a. Test the theory"]]
    F --> G{Was the theory correct?}
    G -.-> |No| C
  end;

  subgraph Resolution & Execution
    D --> E{{"3. Establish a theory<br/>using the OSI Model"}}
    G --> |Yes| Q{{"4. Create an Action Plan<br/>resolve the root cause of<br/>the issue"}}
    Q --> H
    H[["4a. Implement Action Plan and<br/>**VERIFY** the root issue was<br/>resolved"]] --> I[["4b. Implement preventative<br/>measures (if applicable)"]]
  end;

  I --> J

  subgraph Documentation
    J{{**Document:**}}
    J --> K[["1. Issue & steps taken t<br/> resolve issue"]]
    K --> L[["2. Action Plan implementation<br/>and resolution"]]
    L --> M[["3. Preventative measures<br/>implemented"]]
  end;

  M --> N((End))

```



### When to Use Each OSI Approch

| Approach | Starting Layer | Best For |
|----------|---------------|----------|
| **Bottom-Up** | Layer 1 | Initial troubleshooting, no connection to anything |
| **Top-Down** | Layer 7 | Application specific issues, configuration issues |
| **Divide & Conquer** | Layer 3/4 | Unknown root cause, complex issues & systems |


---

## 🚧 Work in Progress

This guide is being actively developed as I progress through CCNA studies and labs. Coming soon:
- [ ] OSI Model Layer-by-Layer Reference Chart
- [ ] Command Reference Table
- [ ] Real Lab Troubleshooting Examples
- [ ] Decision Trees for Common Scenarios
