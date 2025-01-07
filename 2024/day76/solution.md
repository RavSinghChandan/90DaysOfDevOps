# Day 76: Build a Grafana Dashboard - Step-by-Step Solution

## Overview
A Grafana dashboard provides an at-a-glance view of your data, allowing you to track metrics through various visualizations. Follow the steps below to create a dashboard and visualize your data effectively.

---

## Step-by-Step Solution

### Step 1: Create a New Dashboard
1. **Access the Dashboard Creation Menu**:
   - In the sidebar, hover over the **Create (plus sign)** icon.
   - Click on **Dashboard**.

2. **Add a New Panel**:
   - Click the **Add a new panel** button.

---

### Step 2: Configure the Query
1. **Enter the Query**:
   - In the **Query editor** below the graph, enter the following query:
     ```plaintext
     sum(rate(tns_request_duration_seconds_count[5m])) by(route)
     ```
   - Press **Shift + Enter** to execute the query.

2. **Customize the Legend**:
   - In the **Legend field**, enter `{{route}}`.
   - This renames the time series in the legend. Changes will update once you click outside the field.

---

### Step 3: Customize the Panel
1. **Change the Panel Title**:
   - In the **Panel editor** on the right side, locate the **Settings** section.
   - Update the panel title to **Traffic**.

2. **Save the Panel**:
   - Click **Apply** in the top-right corner to save the panel and return to the dashboard view.

---

### Step 4: Save the Dashboard
1. **Save Your Dashboard**:
   - Click the **Save dashboard (disk)** icon at the top of the page.
   - Enter a meaningful name in the **Dashboard name** field.

2. **Finalize**:
   - Click **Save** to store your dashboard.

---

### Additional Tips
- Use the Grafana fundamentals tutorial for more detailed explanations: [Grafana Fundamentals](https://grafana.com/tutorials/grafana-fundamentals/).

- Experiment with different queries and visualizations to build dashboards that meet your specific needs.

---

## Share Your Progress
- Once your dashboard is ready, share a screenshot or description with the community!
- Let's inspire others with amazing dashboards.

[← Previous Day](../day75/README.md) | [Next Day →](../day77/README.md)
