
<h1 align="center">Hi 👋, I'm Vaibhav</h1>
<h3 align="center">A passionate Data Enthusiast from India</h3>

- 🔭 Currently a SDE Intern @Quantbit Technologies Pvt Ltd.

- 🌱 I’m currently learning ** Frappe, Next.js ,Postgres, MySQL, cloud computing, aws env, networking**

-    Check my Blog at https://hashnode.com/@pyvmag

- 👨‍💻 All of my projects are available at [https://github.com/pyvmag](https://github.com/pyvmag)

- 💬 Ask me about **Python , SQL, Tableau, Networking**

- 📫 How to reach me **vaibhavmagdum1528@gmail.com**

<h3 align="left">Connect with me:</h3>
<p align="left">
<a href="https://linkedin.com/in/vaibhav magdum" target="blank"><img align="center" src="https://raw.githubusercontent.com/rahuldkjain/github-profile-readme-generator/master/src/images/icons/Social/linked-in-alt.svg" alt="vaibhav magdum" height="30" width="40" /></a>
</p>

<h3 align="left">Languages and Tools:</h3>
<p align="left"> <a href="https://www.arduino.cc/" target="_blank" rel="noreferrer"> <img src="https://cdn.worldvectorlogo.com/logos/arduino-1.svg" alt="arduino" width="40" height="40"/> </a> <a href="https://www.cprogramming.com/" target="_blank" rel="noreferrer"> <img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/c/c-original.svg" alt="c" width="40" height="40"/> </a> <a href="https://git-scm.com/" target="_blank" rel="noreferrer"> <img src="https://www.vectorlogo.zone/logos/git-scm/git-scm-icon.svg" alt="git" width="40" height="40"/> </a> <a href="https://www.java.com" target="_blank" rel="noreferrer"> <img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/java/java-original.svg" alt="java" width="40" height="40"/> </a> <a href="https://www.mysql.com/" target="_blank" rel="noreferrer"> <img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/mysql/mysql-original-wordmark.svg" alt="mysql" width="40" height="40"/> </a> <a href="https://www.python.org" target="_blank" rel="noreferrer"> <img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/python/python-original.svg" alt="python" width="40" height="40"/> </a> </p>

SELECT
    cw.name,  
    cw.factory_date,
    cw.trip_sheet AS slip_no,
    cw.transporter_contract AS ht_contract,
    cw.transporter_ll_name AS transporter_name,
    cw.route_ll_name AS route_marathi,
    cw.village_ll_name AS village_marathi,
    cw.distance AS distance_marathi,
    MAX(s.custom_ll_name) AS farmer_name_marathi, -- Handles the Duplicate Supplier Issue
    cw.transporter_weight
FROM
    `tabCane Weight` cw
LEFT JOIN 
    `tabSupplier` s ON cw.farmer = s.name
WHERE
    cw.docstatus = 1
    AND cw.season = '2025-2026'                  -- CHANGE THIS
    AND cw.factory_date >= '2025-11-01'          -- CHANGE THIS
    AND cw.factory_date <= '2025-11-15'          -- CHANGE THIS
    -- AND cw.transporter_contract = 'HTC...'    -- OPTIONAL
GROUP BY
    cw.name   -- <--- THE CRITICAL FIX (Prevents Duplicates)
ORDER BY
    cw.transporter_ll_name, cw.factory_date, cw.trip_sheet



SELECT 
    COUNT(*) as total_rows_after_fix,
    ROUND(SUM(fixed_data.transporter_weight), 3) as FINAL_GRAND_TOTAL
FROM (
    SELECT
        cw.name,
        cw.transporter_weight
    FROM
        `tabCane Weight` cw
    LEFT JOIN 
        `tabSupplier` s ON cw.farmer = s.name
    WHERE
        cw.docstatus = 1
        AND cw.season = '2025-2026'              -- CHANGE THIS
        AND cw.factory_date >= '2025-11-01'      -- CHANGE THIS
        AND cw.factory_date <= '2025-11-15'      -- CHANGE THIS
    GROUP BY
        cw.name -- <--- THE CRITICAL FIX
) as fixed_data;

<!--
**pyvmag/pyvmag** is a ✨ _special_ ✨ repository because its `README.md` (this file) appears on your GitHub profile.

Here are some ideas to get you started:

- 🔭 I’m currently working on ...
- 🌱 I’m currently learning ...
- 👯 I’m looking to collaborate on ...
- 🤔 I’m looking for help with ...
- 💬 Ask me about ...
- 📫 How to reach me: ...
- 😄 Pronouns: ...
- ⚡ Fun fact: ...
-->
