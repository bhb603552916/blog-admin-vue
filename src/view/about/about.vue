<template>
  <div class="container">
    <div class="lin-info">
      <div class="lin-info-left">
        <div class="welcome">
          <p class="welcome-title">LRboy Blog 后台管理系统</p>
          <!-- <img src="../../assets/image/about/welcome.png" class="welcome-title" alt="" /> -->
          <div class="subtitle">
            <div class="guide">您还可以点击查看我的GitHub仓库，查看更多作品</div>
            <div class="link">
              <a href="https://www.talelin.com" target="_blank">https://github.com/bhb603552916</a>
            </div>
          </div>
        </div>
        <img class="welcome-bg" src="../../assets/image/about/header-bg.png" alt />
      </div>
      <div class="lin-info-right">
        <div class="team-detail">
          <div class="team-box">
            <div class="team-title">产品团队</div>
            <ul class="team-ul">
              <li>
                <span class="shadow-box">
                  <i class="team-shadow"></i>
                </span>
                <span class="team-role">策划</span>
                <span class="team-name">LRboy</span>
              </li>
              <li>
                <span class="shadow-box">
                  <i class="team-shadow"></i>
                </span>
                <span class="team-role">研发</span>
                <span class="team-name">LRboy</span>
              </li>
              <li>
                <span class="shadow-box">
                  <i class="team-shadow"></i>
                </span>
                <span class="team-role">设计</span>
                <span class="team-name">林间有风团队</span>
              </li>
            </ul>
          </div>
        </div>
      </div>
    </div>
    <div class="quantity-statistics">
      <div class="quantity-item">
        <div class="quantity-detail">
          <div class="quantity-detail-box">
            <div class="quantity-title">总访问量</div>
            <div class="quantity-border-line"></div>
            <div class="quantity">1660</div>
          </div>
        </div>
        <div class="quantity-icon">
          <img src="../../assets/image/about/icon.png" alt />
        </div>
      </div>
      <div class="quantity-item">
        <div class="quantity-detail">
          <div class="quantity-detail-box">
            <div class="quantity-title">总用户数</div>
            <div class="quantity-border-line"></div>
            <div class="quantity">52</div>
          </div>
        </div>
        <div class="quantity-icon">
          <img src="../../assets/image/about/icon.png" alt />
        </div>
      </div>
      <div class="quantity-item">
        <div class="quantity-detail">
          <div class="quantity-detail-box">
            <div class="quantity-title">新增访问量 (月)</div>
            <div class="quantity-border-line"></div>
            <div class="quantity">182</div>
          </div>
        </div>
        <div class="quantity-icon">
          <img src="../../assets/image/about/icon.png" alt />
        </div>
      </div>
      <div class="quantity-item">
        <div class="quantity-detail">
          <div class="quantity-detail-box">
            <div class="quantity-title">新增用户数</div>
            <div class="quantity-border-line"></div>
            <div class="quantity">13</div>
          </div>
        </div>
        <div class="quantity-icon">
          <img src="../../assets/image/about/icon.png" alt />
        </div>
      </div>
    </div>
    <div class="information">
      <div class="personal">
        <div class="personal-title">个人信息</div>
        <img src="http://www.lrboy.live/2020/06/24/c33eee2c-b5f5-11ea-929c-f45c89cb3825.jpg" class="personal-avatar" />
        <div class="personal-influence">
          <div class="personal-influence-item">
            <div class="personal-influence-num color1">0</div>
            <div class="personal-influece-label">总访问量</div>
          </div>
          <div class="personal-influence-item">
            <div class="personal-influence-num color2">0</div>
            <div class="personal-influece-label">粉丝</div>
          </div>
          <div class="personal-influence-item">
            <div class="personal-influence-num color3">5</div>
            <div class="personal-influece-label">作品</div>
          </div>
        </div>
        <el-tabs v-model="activeName" class="personal-tabs">
          <el-tab-pane label="最新作品" name="first">
            <p class="content">
              <a href="https://github.com/bhb603552916/lrblog-vue" target="_blank">LRBlog(已上线)</a>
            </p>
            <p class="content">
              <a href="https://github.com/bhb603552916/blog-admin-vue" target="_blank">LRBlog-CMS(已上线)</a>
            </p>
          </el-tab-pane>
          <el-tab-pane label="其他作品" name="second">
            <p class="content">敬请期待...</p>
          </el-tab-pane>
        </el-tabs>
      </div>
      <div class="article">
        <div class="article-title">文章</div>
        <div class="article-list">
          <div class="article-item" v-for="(item, index) in articles" :key="index">
            <img class="article-thumb" :src="item.banner" alt />
            <div class="article-detail article-last">
              <p class="article-detail-title">{{ item.title }}</p>
              <div class="article-detail-content">
                {{ item.introduction }}
              </div>
              <div class="article-tool">
                <div class="pubdate">{{ item.pub_time }}</div>
                <div class="article-about">
                  <span> <i class="iconfont icon-shoucang"></i>{{ item.likes }}</span>
                  <el-divider direction="vertical"></el-divider>
                  <span> <i class="iconfont icon-pinglun"></i>{{ item.commentsCount }}</span>
                  <el-divider direction="vertical"></el-divider>
                  <span> <i class="el-icon-view" style="margin-right: 5px;"></i>{{ item.views }} </span>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
/* eslint-disable */
import articleApi from '../../model/article'
export default {
  data() {
    return {
      activeName: 'first',
      showTeam: false,
      articles: [],
    }
  },
  mounted() {
    this.getArticles()
    if (document.body.clientWidth > 1200 && document.body.clientWidth < 1330) {
      this.showTeam = true
    }
  },
  methods: {
    async getArticles() {
      try {
        this.loading = true
        const res = await articleApi.getArticles({
          count: 3,
          page: 1,
        })
        this.articles = res.articles
        console.log(res)
      } catch (e) {
        console.log(e)
      }
    },
  },
}
</script>

<style scoped lang="scss">
.container {
  padding: 20px;
  .lin-info {
    display: flex;
    flex: 1;
    height: 160px;
    width: 100%;
    .lin-info-left {
      position: relative;
      width: 690px;
      height: 100%;
      background: rgba(69, 119, 255, 1);
      box-shadow: 0px 2px 14px 0px rgba(243, 243, 243, 1);
      border-radius: 8px;
      .welcome {
        margin: 28px 0 0 30px;
        .welcome-title {
          margin-bottom: 30px;
          color: #fff;
          font-weight: bold;
          font-size: 24px;
        }
        .subtitle {
          display: flex;
          flex-direction: column;
          margin-top: 16px;
          color: #fff;
          .guide {
            margin-right: 20px;
            font-size: 14px;
            font-weight: 400;
            line-height: 20px;
          }
          .link {
            font-size: 14px;
            padding: 2px 0px;
            margin-top: 15px;
            width: 260px;
            height: 22px;
            background: rgba(44, 95, 233, 1);
            border-radius: 11px;
            text-align: center;
            line-height: 20px;
            color: rgba(255, 255, 255, 1);
          }
        }
      }
      .welcome-bg {
        position: absolute;
        bottom: 0;
        right: 10px;
        width: 393px;
        height: 121px;
      }
    }
    .lin-info-right {
      flex: 1;
      margin-left: 20px;
      height: 100%;
      display: flex;
      flex-direction: column;
      .team-detail {
        position: relative;
        height: 160px;
        background: rgba(255, 176, 139, 1);
        box-shadow: 0px 2px 14px 0px rgba(243, 243, 243, 1);
        border-radius: 8px;
        .team-box {
          margin: 20px 0 0 22px;
          .team-ul {
            margin-top: 15px;
            li {
              height: 20px;
              line-height: 20px;
              margin-bottom: 15px;
              font-size: 14px;
              .shadow-box {
                position: relative;
                display: inline-block;
                margin-right: 10px;
                width: 14px;
                height: 14px;
                border-radius: 14px;
                background-color: #fff;
                transform: translateY(2px);
                .team-shadow {
                  position: absolute;
                  top: 25%;
                  left: 25%;
                  display: inline-block;
                  width: 6px;
                  height: 6px;
                  border-radius: 6px;
                  background-color: #ffb9a4;
                }
              }
              .team-role {
                display: inline-block;
                width: 30px;
                margin-right: 15px;
                font-weight: 400;
                color: #45526b;
              }
              .team-name {
                font-weight: 400;
                color: #fff;
                ul {
                  display: inline;
                  li {
                    display: inline;
                    margin-right: 15px;
                  }
                }
              }
            }
          }
        }
        .team-icon {
          position: absolute;
          top: 25%;
          right: 33px;
          width: 70px;
          height: 70px;
          display: flex;
          justify-content: center;
          align-items: center;
          background-color: #fff;
          box-shadow: 0 0 10px 0 #cfd5e3;
          img {
            width: 62px;
            height: 62px;
          }
        }
        .team-label {
          position: absolute;
          top: 73%;
          right: 20px;
          font-size: 13px;
          font-weight: 400;
          color: rgba(69, 82, 107, 1);
          line-height: 20px;
        }
      }
    }
  }
  .quantity-statistics {
    display: flex;
    justify-content: space-between;
    margin-top: 20px;
    height: 90px;
    .quantity-item {
      display: flex;
      width: 23%;
      height: 100%;
      background: rgba(255, 255, 255, 1);
      box-shadow: 0px 2px 14px 0px rgba(243, 243, 243, 1);
      border-radius: 8px;
      .quantity-detail {
        flex: 1;
        .quantity-detail-box {
          margin: 12px 0 0 30px;
          .quantity-title {
            margin-bottom: 2px;
            height: 20px;
            line-height: 20px;
            color: #495468;
            font-size: 14px;
            font-weight: 400;
          }
          .quantity-border-line {
            width: 46px;
            height: 2px;
            background: rgba(73, 84, 104, 1);
          }
          .quantity {
            margin-top: 7px;
            height: 48px;
            font-size: 32px;
            color: rgba(73, 84, 104, 1);
            line-height: 38px;
            letter-spacing: 2px;
          }
        }
      }
      .quantity-icon {
        display: flex;
        justify-content: center;
        align-items: center;
        width: 90px;
        height: 100%;
        background: rgba(69, 119, 255, 0.1);
        border-top-right-radius: 8px;
        border-bottom-right-radius: 8px;
        img {
          width: 28px;
          height: 33px;
        }
      }
    }
  }
  .information {
    margin-top: 20px;
    display: flex;
    .personal {
      width: 320px;
      height: 100%;
      margin-right: 20px;
      background: rgba(255, 255, 255, 1);
      box-shadow: 0px 2px 14px 0px rgba(243, 243, 243, 1);
      border-radius: 8px;
      .personal-title {
        margin: 20px 0 10px 20px;
        height: 22px;
        line-height: 22px;
        font-weight: 500;
        color: #596c8e;
        font-size: 16px;
      }
      .personal-avatar {
        width: 140px;
        height: 140px;
        margin: 0 auto 40px;
        border-radius: 75px;
        box-shadow: 0 0 30px 0 #cfd5e3;
      }
      .personal-influence {
        display: flex;
        justify-content: space-between;
        padding: 0 30px 40px;
        .personal-influence-item {
          display: flex;
          flex-direction: column;
          align-items: center;
          .personal-influence-num {
            font-size: 28px;
            line-height: 34px;
            &.color1 {
              color: #00c292;
            }
            &.color2 {
              color: #fec108;
            }
            &.color3 {
              color: #03a9f3;
            }
          }
          .personal-influece-label {
            font-size: 12px;
            font-weight: 400;
            color: #8c98ae;
            line-height: 17px;
          }
        }
      }
      .personal-tabs {
        margin-bottom: 20px;
        .content {
          padding: 10px;
          line-height: 20px;
          > a {
            font-style: italic;
            font-size: 14px;
          }
          > a:hover {
            color: #3963bc;
            font-weight: bold;
          }
        }
      }
      .personal-tabs /deep/ .is-top {
        width: 320px;
        display: flex;
        justify-content: space-around;
      }
      .personal-tabs /deep/ .el-tabs__content {
        text-indent: 20px;
      }
    }
    .article {
      flex: 1;
      height: 100%;
      padding: 20px;
      background: rgba(255, 255, 255, 1);
      box-shadow: 0px 2px 14px 0px rgba(243, 243, 243, 1);
      border-radius: 8px;
      .article-title {
        height: 22px;
        line-height: 22px;
        font-weight: 500;
        color: #596c8e;
        font-size: 16px;
        margin-bottom: 20px;
      }
      .article-list {
        cursor: pointer;
        .article-item {
          display: flex;
          flex-direction: row;
          justify-content: flex-start;
          .article-thumb {
            width: 120px;
            height: 120px;
            border-radius: 8px;
            margin-right: 30px;
          }
          .article-detail {
            flex: 1;
            border-bottom: 1px #ecedef solid;
            margin-bottom: 20px;
            &.article-last {
              border-bottom: none;
              margin-bottom: 0;
            }
            .article-detail-title {
              height: 22px;
              font-size: 16px;
              font-weight: 400;
              color: rgba(69, 82, 107, 1);
              line-height: 22px;
            }
            .article-detail-content {
              margin-top: 10px;
              font-size: 14px;
              font-weight: 400;
              color: rgba(140, 152, 174, 1);
              line-height: 22px;
            }
          }
          .article-tool {
            display: flex;
            flex-direction: row;
            justify-content: space-between;
            margin: 10px 0 20px 0;
            font-size: 12px;
            line-height: 17px;
            font-weight: 400;
            color: #808da3;
            .article-about {
              .iconfont {
                line-height: 17px;
                margin-right: 6px;
                font-size: 12px;
              }
            }
          }
        }
      }
    }
  }
}

@media screen and (max-width: 1200px) {
  .container .lin-info .lin-info-right {
    display: none;
  }
  .container .lin-info .lin-info-left {
    width: 100%;
  }
  .container .quantity-statistics .quantity-item {
    width: 32%;
    &:last-child {
      display: none;
    }
  }
  .container .information .personal {
    display: none;
  }
}

@media screen and (max-width: 1200px) {
  .container .lin-info .lin-info-left {
    width: 100%;
  }
}
</style>
