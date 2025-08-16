EDIT: forked from ramkumar-kr/containers-sync, which at the time of this writing has been not modified since 2019 - 6 years ago.
Firefox provides container syncing - or tries to do so. Problem is it is utterly **broken** when using multiples devices:
- it generates multiple duplicates
- anything referring to containers (e.g. default container for new tabs) is associated differently in different devices; meanning, if I config device A to open tabs on container X in my account, when I go to device B setting is instead configured to open tabs on container Y. If I change device B to open tabs on container X as I originally wanted, when I go back to device A now it is set to open in container Z...

Therefore, since Firefox's default container syncing mechanism seems uterly **broken**, with no hope of being fixed, by idea is to provide a separate syncing mechanism.

I suspect containers are copied by name between devices, but IDs end up being different somehow. Possible solutions:
1. Enforce same IDs across devices.
2. If 1. is not possible, then use container names and not IDs for any type of container aassociation.

Since I use Zen Browser, I will also attempt to check if running browser is Zen; if that is the case, I will take care of extra scenarios, such as workspace vs container association too.

---

# Containers Sync

This is a webextension which would sync firefox containers across multiple devices.

[![Get-the-addon-button](https://addons.cdn.mozilla.net/static/img/addons-buttons/AMO-button_1.png)](https://addons.mozilla.org/en-US/firefox/addon/containers-sync/)

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
    
    No. This data is not available to any extensions by the API.

- **Will this extension work with firefox for android?**

    No

- **Will this extension work in chrome/opera/edge etc.,?**

    No

- **I have some feedback...**

    You can create an issue in Github and we can discuss about it
