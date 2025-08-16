# Containers Sync *Fix*

This is a webextension which would **fix** sync firefox containers across multiple devices.

---

## 2025-08-16

This repo was forked from [ramkumar-kr/containers-sync](https://github.com/ramkumar-kr/containers-sync), which has the sole purpose of implementing container syncing across devices, and which has not been updated since 2019 (6 years ago).

Currently, Firefox *does* provide a default container syncing mechanism — or at least it *tries to*.  
The problem is that syncing across multiple devices is utterly **broken**:

- It creates endless duplicates.  
- Container-related settings (e.g. default container for new tabs) are inconsistent between devices. For example:  
  - On device A, I configure new tabs to open in container **X**.  
  - On device B, the same setting is instead mapped to container **Y**.  
  - If I fix device B to use container **X**, when I return to device A the setting has now shifted to container **Z**…  

Because Firefox’s built-in container syncing ends up causing more issues than solving, with little hope of being fixed, my idea is to provide an alternative syncing mechanism.

I suspect that while containers are copied by *name* across devices, their **IDs** end up mismatched.  

### Possible solutions

1. Enforce the same container IDs across devices.  
2. If (1) is not possible, use container **names** instead of IDs for any container association.  

Since I use **Zen Browser**, I will also check whether the running browser is Zen. In that case, I’ll handle extra scenarios, such as workspace ↔ container associations.

---

## Steps to build

* Use node 10.16.1 and npm 6.11.3 only
* Clone the repository (`git clone git@github.com:ramkumar-kr/containers-sync.git`)
* Run npm install in the containers-sync directory to install all dependencies (`npm install`)
* Run `webpack` to generate the `dist` directory
* You can use [github actions file](./.github/workflows/nodejs.yml) as a reference for an automated script

### Testing the extension
* Run `npm run watch` to start webpack to generate the dist directory
* Run `npm run firefox` to load the extension to firefox  with a temporary profile

### Building for production
* Use ubuntu 18.04 LTS only
* Run `npm run production`
* Upload the zip file in the web-ext-artiacts directory to the addon store

## FAQ

-  **What does this extension do?**

    It will synchronize the name, icon and colour of containers across devices

- **How frequently do you backup?**

  - As soon as you create/update/remove a container or multiple containers
  - Whenever the backup button is clicked in the popup
  
- **Is it possible to view the list of synced containers?**
    
    Yes. You can view the list of synced containers by clicking on the "View synced containers" button or from the sidebar.


- **Can I backup/restore them manually?**

    Yes. You can use the popup to backup or restore manually

-  **I have set a preference to open a website in a particular container. Will that also be synced?**
    
    ~No. This data is not available to any extensions by the API.~ 2025: I don't think that's the case anymore, so I will try to implement this feature too.

- **Will this extension work with firefox for android?**

    No

- **Will this extension work in chrome/opera/edge etc.,?**

    No

- **I have some feedback...**

    You can create an issue in Github and we can discuss about it
