
<template>
  <div id="q-app">
    <router-view />
  </div>
</template>
<script>
import {
  Loading,
  QSpinnerGears
} from 'quasar'

export default {
  
  name: 'App',
    //Prefetching on ServerSide of initial data, it fills Our vuex store.
    preFetch ({ store, currentRoute, previousRoute, redirect, ssrContext, urlPath, publicPath }) {
    // fetch data, validate route and optionally redirect to some other route...
    // ssrContext is available only server-side in SSR mode

    // No access to "this" here

    ssrContext['$q'].lang.isoName = 'es'
    ssrContext['$q'].lang.nativeName = 'Español (ES)'
    ssrContext.Q_HTML_ATTRS = 'lang=es dir=ltr'
    ssrContext.Q_PREV_LANG = 'lang=es dir=ltr'

    // Return a Promise if you are running an async job
    return Promise.all([
      store.dispatch('internalSections/actionInternalSections'),
      store.dispatch('categories/actionCategories'),
      store.dispatch('categories/actionSubCategories'),
      store.dispatch('products/actionProducts'),
      store.dispatch('extra/actionContact'),
      store.dispatch('extra/actionSocialNetworks'),
      store.dispatch('home/actionHome'),
      ])
      
    },
    mounted(){
      window.addEventListener('popstate', () => {
        Loading.show()
        location.reload();
      })
    }
}
</script>
