import router from './router'
import store from './store'
import NProgress from 'nprogress' // progress bar
import 'nprogress/nprogress.css' // progress bar style
import { getToken, setToken, removeToken, ssoAuth, logout } from '@/utils/auth' // get token from cookie
import { getQueryByParams } from '@/utils/assist'
import { init } from '@/api/user'
import getPageTitle from '@/utils/get-page-title'

NProgress.configure({ showSpinner: false }) // NProgress Configuration

const whiteList = ['/404', '/403', '/500'] // no redirect whitelist

function handleRouter (to, next) {
  next()
}

function scrollToTop () {
  let mainElm = document.body.querySelector('.mp-main')
  if (mainElm) {
    let step = 0
    let interval = setInterval(() => {
      if (mainElm.scrollTop <= 0) {
        clearInterval(interval)
        return
      }
      step += 10
      mainElm.scrollTop -= step
    }, 20)
  }
}

router.beforeEach(async (to, from, next) => {
  // start progress bar
  NProgress.start()
  // 返回页面顶部
  scrollToTop()
  // set page title
  document.title = getPageTitle(to.meta.title)
  // determine whether the user has logged in
  // 无token相关信息，跳转到sso登陆页面

  const hasToken = getToken()
  if (whiteList.indexOf(to.path) !== -1) {
    NProgress.done()
    next()
  } else {
    let token = getQueryByParams('token')
    if (token || hasToken) {
      // 去验证Token是否正确
      if (token) {
        console.log('进入1')
        setToken(token)
        store.commit('user/SET_TOKEN', token)
        let path = window.location.pathname
        // 去掉token参数
        window.history.pushState(null, null, '/')
        next({ path })
      } else {
        console.log('进入2')
        setToken(hasToken)
        store.commit('user/SET_TOKEN', hasToken)
        // 判断是否存在用户信息
        if (!store.state.user.userAccount) {
          init().then(res => {
            if (res && res.code === 0) {
              // 设置state中的值
              store.commit('user/SET_USERINFO', res.data)
              handleRouter(to, next)
              NProgress.done()
            } else {
              removeToken()
              logout()
            }
          }).catch(error => {
            console.log(error)
            // 调试用
            let path = window.location.pathname
            next({ path: path })
            NProgress.done()
            // removeToken()
            // logout()
          })
        } else {
          // 不是tb用户无法查看视图
          handleRouter(to, next)
          NProgress.done()
        }
      }
    } else {
      ssoAuth()
    }
  }
})

router.afterEach(() => {
  // finish progress bar
  NProgress.done()
})
