[![hacs_badge](https://img.shields.io/badge/HACS-Default-orange.svg?style=for-the-badge)](https://github.com/custom-components/hacs)  

# tab-redirect-card
Custom [Lovelace](https://www.home-assistant.io/lovelace) card to use in [Home assistant](https://www.home-assistant.io/) allowing you to redirect a user to certain view based on entity states.  
You can see it as a way to set the default tab based on entity states.  

A common use-case is to put the card on the default view and have it redirecting you under some conditions.  

For instance:
- If sun is below_horizon you want the default view to be the tab controlling the lights
- But when you are outside, you want the default view to be tab with the cameras
- Rest of the time, the default view should be the regular default view (aka no redirect)

### Installation
Use [HACS](https://hacs.xyz/) or follow this [guide](https://github.com/thomasloven/hass-config/wiki/Lovelace-Plugins)

```
resources:
  url: /local/tab-redirect-card.js
  type: module
```

### Configuration example:
Note: `redirect_to_tab_index` starts at 0 (first tab)  

 - Redirect user "foo" to the 2nd tab if `input.binary.is_home` is `on`:
```yaml
type: 'custom:tab-redirect-card'
redirect:
 - user: 'foo'
   entity_id: 'input.binary.is_home'
   entity_state: 'on'
   redirect_to_tab_index: 1
```

 - Redirect user "foo" to the 2nd tab if `input.binary.is_home` is `on`  
   And redirect user "bar" to the 3rd tab if `input.binary.is_home` is `on`  
```yaml
type: 'custom:tab-redirect-card'
redirect:
 - user: 'foo'
   entity_id: 'input.binary.is_home'
   entity_state: 'on'
   redirect_to_tab_index: 1
 - user: 'bar'
   entity_id: 'input.binary.is_home'
   entity_state: 'on'
   redirect_to_tab_index: 2
```
N.B If using panel mode, your tab-redirect-cards must be positioned in the first row otherwise they won't work. Don't worry, the card/s won't be visible when you exit edit mode.
