<template>
  <div class="row">
    <div class="col-md-6">
      <card>
        <h4 slot="header" class="card-title">Notifications Style</h4>

        <BaseAlert type="info"> This is a plain notification</BaseAlert>

        <BaseAlert type="info" dismissible> This is a notification with close button. </BaseAlert>

        <BaseAlert type="info" dismissible icon="tim-icons icon-bell-55">
          This is a notification with close button and icon.
        </BaseAlert>

        <BaseAlert type="info" dismissible icon="tim-icons icon-bell-55">
          This is a notification with close button and icon and have many lines. You can see that the icon and the close
          button are always vertically aligned. This is a beautiful notification. So you don't have to worry about the
          style.
        </BaseAlert>
      </card>
    </div>

    <div class="col-md-6">
      <card>
        <h4 slot="header" class="card-title">Notification states</h4>

        <BaseAlert type="primary" dismissible>
          <span><b> Primary - </b> This is a regular notification made with ".alert-primary"</span>
        </BaseAlert>

        <BaseAlert type="info" dismissible>
          <span><b> Info - </b> This is a regular notification made with ".alert-info"</span>
        </BaseAlert>

        <BaseAlert type="success" dismissible>
          <span><b> Success - </b> This is a regular notification made with ".alert-success"</span>
        </BaseAlert>

        <BaseAlert type="warning" dismissible>
          <span><b> Warning - </b> This is a regular notification made with ".alert-warning"</span>
        </BaseAlert>

        <BaseAlert type="danger" dismissible>
          <span><b> Danger - </b> This is a regular notification made with ".alert-danger"</span>
        </BaseAlert>
      </card>
    </div>
    <div class="col-md-12">
      <card class="text-center">
        <div class="places-buttons">
          <div class="row">
            <div class="col-md-6 ml-auto mr-auto text-center">
              <h4 class="card-title">
                Notifications Places
                <p class="category">Click to view notifications</p>
              </h4>
            </div>
          </div>
          <div class="row">
            <div class="col-lg-8 ml-auto mr-auto">
              <div class="row">
                <div class="col-md-4">
                  <BaseButton type="primary" block @click.native="notifyVue('top', 'left')">Top Left </BaseButton>
                </div>
                <div class="col-md-4">
                  <BaseButton type="primary" block @click.native="notifyVue('top', 'center')">Top Center </BaseButton>
                </div>
                <div class="col-md-4">
                  <BaseButton type="primary" block @click.native="notifyVue('top', 'right')">Top Right </BaseButton>
                </div>
              </div>
            </div>
          </div>
          <div class="row">
            <div class="col-lg-8 ml-auto mr-auto">
              <div class="row">
                <div class="col-md-4">
                  <BaseButton type="primary" block @click.native="notifyVue('bottom', 'left')">Bottom Left </BaseButton>
                </div>
                <div class="col-md-4">
                  <BaseButton type="primary" block @click.native="notifyVue('bottom', 'center')"
                    >Bottom Center
                  </BaseButton>
                </div>
                <div class="col-md-4">
                  <BaseButton type="primary" block @click.native="notifyVue('bottom', 'right')"
                    >Bottom Right
                  </BaseButton>
                </div>
              </div>
            </div>
          </div>
        </div>

        <div class="row">
          <div class="col-md-12 text-center">
            <div class="card-header"><h4 class="card-title">Modal</h4></div>

            <BaseButton type="primary" @click.native="modals.classic = true"> Classic modal </BaseButton>
            &nbsp;
            <BaseButton type="info" @click.native="modals.notice = true"> Notice modal </BaseButton>
            &nbsp;
            <BaseButton @click.native="modals.mini = true"> Small alert modal </BaseButton>

            <!-- Classic Modal -->
            <Modal :show.sync="modals.classic" header-classes="justify-content-center">
              <h4 slot="header" class="title title-up">Modal title</h4>
              <p>
                Far far away, behind the word mountains, far from the countries Vokalia and Consonantia, there live the
                blind texts. Separated they live in Bookmarksgrove right at the coast of the Semantics, a large language
                ocean. A small river named Duden flows by their place and supplies it with the necessary regelialia. It
                is a paradisematic country, in which roasted parts of sentences fly into your mouth.
              </p>
              <template slot="footer">
                <BaseButton>Nice Button</BaseButton>
                <BaseButton type="danger" @click.native="modals.classic = false">Close </BaseButton>
              </template>
            </Modal>

            <!-- notice modal -->
            <Modal :show.sync="modals.notice" footer-classes="justify-content-center" type="notice">
              <h5 slot="header" class="modal-title"> How Do You Become an Affiliate? </h5>
              <div class="instruction">
                <div class="row">
                  <div class="col-md-8">
                    <strong>1. Register</strong>
                    <p class="description">
                      The first step is to create an account at
                      <a href="http://www.creative-tim.com/">Creative Tim</a>. You can choose a social network or go for
                      the classic version, whatever works best for you.
                    </p>
                  </div>
                  <div class="col-md-4">
                    <div class="picture">
                      <img src="img//bg1.jpg" alt="Thumbnail Image" class="rounded img-raised" />
                    </div>
                  </div>
                </div>
              </div>
              <div class="instruction">
                <div class="row">
                  <div class="col-md-8">
                    <strong>2. Apply</strong>
                    <p class="description">
                      The first step is to create an account at
                      <a href="http://www.creative-tim.com/">Creative Tim</a>. You can choose a social network or go for
                      the classic version, whatever works best for you.
                    </p>
                  </div>
                  <div class="col-md-4">
                    <div class="picture">
                      <img src="img//bg3.jpg" alt="Thumbnail Image" class="rounded img-raised" />
                    </div>
                  </div>
                </div>
              </div>
              <p>
                If you have more questions, don't hesitate to contact us or send us a tweet @creativetim. We're here to
                help!
              </p>
              <div slot="footer" class="justify-content-center">
                <BaseButton type="info" round @click.native="modals.notice = false">Sounds good! </BaseButton>
              </div>
            </Modal>

            <!-- small modal -->
            <Modal
              :show.sync="modals.mini"
              class="modal-primary"
              :show-close="false"
              header-classes="justify-content-center"
              type="mini"
            >
              <div slot="header" class="modal-profile">
                <i class="tim-icons icon-single-02"></i>
              </div>
              <p>Always have an access to your profile</p>
              <template slot="footer">
                <BaseButton type="neutral" link>Back</BaseButton>
                <BaseButton type="neutral" link @click.native="modals.mini = false">Close </BaseButton>
              </template>
            </Modal>
          </div>
        </div>
      </card>
    </div>
  </div>
</template>
<script>
  import { Modal, BaseAlert } from '@/components';

  export default {
    name: 'Notifications',
    components: {
      Modal,
      BaseAlert,
    },
    data() {
      return {
        type: ['', 'info', 'success', 'warning', 'danger'],
        notifications: {
          topCenter: false,
        },
        modals: {
          classic: false,
          notice: false,
          mini: false,
        },
      };
    },
    methods: {
      notifyVue(verticalAlign, horizontalAlign) {
        const color = Math.floor(Math.random() * 4 + 1);
        this.$notify({
          message: 'Welcome to <b>Vue Black Dashboard Pro</b> - a beautiful resource for every web developer',
          timeout: 30000,
          icon: 'tim-icons icon-bell-55',
          horizontalAlign,
          verticalAlign,
          type: this.type[color],
        });
      },
    },
  };
</script>
<style>
  .card .alert {
    position: relative !important;
    width: 100%;
  }
</style>
