# Empty Recycle Bin Automatically

## Steps

### Create a Task

1. Log in to Synology DiskStation Manager.
2. Open **Control Panel**.
3. Under **Services**, open **Task Scheduler**.
4. Click **Create** → **Scheduled Task** → **Recycle Bin**.

### Configure the Task

5. In the **General** tab, enter a task name and select **Enabled**.
6. In the **Schedule** tab, set the date and time.

    > **Example:** For monthly cleanup on the last Sunday at midnight, select **Monthly**, **Last**, and **Sunday**, and set **Start time** to `00:00`.

7. In the **Task Settings** tab, select the recycle bins and file types to delete.
8. If needed, click **Advanced Settings** for additional options.
9. Click **OK**, then **Yes** in the confirmation dialog.