<template>
  <div class="s1-loc__container">
    <div class="s1-U__mg--bt32">
      <div class="md-display-1 s1-U__text-color--dark-2 s1-U__align-children--center">
        <md-button
          class="md-dense md-icon-button s1-U__mg--rt16 s1-U__mg--tp16"
          @click="setActivePage('users-by-account')"
        >
          <md-icon>arrow_back</md-icon>
        </md-button>
        <div>
          <p class="md-caption s1-U__fw--300 s1-U__text-color--dark-2">ICATU MV/ VENDAS</p>
          <h1 class="md-display-1 s1-U__text-color--dark-2 s1-U__align-children--center">
            <span>Cadastro de usuário</span>
          </h1>
        </div>
      </div>
    </div>

    <md-card class="s1-loc__width--900px">
      <md-card-content>
        <div>
          <!-- <h3 class="md-title s1-U__text-color--primary s1-U__mg--tp4">Dados cadastrais</h3> -->
          <div class="s1-U__pd--tp4">
            <div class="s1-loc__md-field-wrapper s1-U__width--300px">
              <md-field>
                <label>Primeiro Nome</label>
                <md-input v-model="form.FirstName" required/>
              </md-field>
            </div>

            <div class="s1-loc__md-field-wrapper s1-U__width--300px">
              <md-field>
                <label>Sobrenome</label>
                <md-input v-model="form.LastName" required/>
              </md-field>
            </div>

            <div class="s1-loc__md-field-wrapper s1-U__width--300px">
              <md-field>
                <label>Username (login)</label>
                <md-input v-model="form.Username" required/>
                <span class="md-suffix">@icatu</span>
              </md-field>
            </div>

            <div class="s1-loc__md-field-wrapper s1-U__width--300px">
              <md-field>
                <label>Email</label>
                <md-input v-model="form.Email"/>
              </md-field>
            </div>

            <div class="s1-loc__md-field-wrapper s1-U__width--300px">
              <md-field>
                <label>Senha</label>
                <md-input v-model="form.Password" type="password"/>
              </md-field>
            </div>

            <div class="s1-loc__md-field-wrapper s1-U__width--300px">
              <md-field>
                <label>Confirmar senha</label>
                <md-input v-model="form.ConfirmPassword" type="password"/>
              </md-field>
            </div>

            <!-- <md-button
              class="md-primary s1-md-bordered s1-U__mg--bt24 s1-U__mg--tp16"
              @click="setShowPasswordDialog"
            >alterar senha</md-button>-->
          </div>
          <h3 class="md-title s1-U__pd--tp32 s1-U__text-color--primary">Perfis de acesso</h3>
          <!--<p class="s1-U__pd--tp8 s1-U__mg--bt16 md-caption">
            Para ter acesso ao sistema, o usuário precisa de pelo menos
            <b>um perfil</b> em
            <b>uma conta</b> para login.
          </p>-->
          <div class="s1-U__pd--lt16 s1-U__mg--tp16">
            <div class="s1-U__align-children--center s1-U__mg--tp8 s1-U__mg--bt16">
              <img
                src="https://s1-cdn-brazilsouth.azureedge.net/sales.svg"
                style="width: 24px; height: 24px;"
                alt
              >
              <p class="md-body-2 s1-U__mg--lt8">Vendas</p>
            </div>
            <div class="s1-U__width--320px">
              <table class="s1-U__full-width" style="border-spacing: 0">
                <tr>
                  <td class="s1-U__text-color--dark-2">Icatu MV</td>
                  <td class="s1-U__pd--lt8 s1-U__pd--rt8 s1-U__text-align--center">
                    <div class="s1-U__vertical-divider" style="display: inline-block"/>
                  </td>
                  <td class="s1-U__pd--tp4 s1-U__pd--bt4">
                    <div class="s1-loc__md-field-wrapper">
                      <md-field class="s1-U__mg0">
                        <label for>Perfil</label>
                        <md-select v-model="form.AccountsProfile1">
                          <md-option value="Admin">Administrador</md-option>
                          <md-option value="Normal">Normal</md-option>
                          <md-option value="Mui loko">Mui loko</md-option>
                        </md-select>
                      </md-field>
                    </div>
                  </td>
                </tr>
              </table>
            </div>
          </div>
        </div>
      </md-card-content>

      <md-card-actions class="s1-U__pd16">
        <md-button class="md-raised md-primary" @click="showDialogProfileOption = true">Salvar</md-button>
      </md-card-actions>
    </md-card>
    <md-dialog :md-active.sync="showDialogProfileOption">
      <md-content>
        <p>
          Deseja configurar agora o perfil de acesso a
          <b>Icatu MV/ Vendas</b>? Sem acesso ao
          <b>Accounts</b>, por exemplo, o usuário será
          <b>incapaz de fazer login.</b>
        </p>
      </md-content>
      <md-dialog-actions class="s1-U__pd16 s1-U__pd--tp0 s1-U__text-align--right">
        <md-button
          class="md-primary s1-md-bordered"
          @click="setActivePage('users-by-account')"
        >deixar para depois</md-button>
        <md-button
          class="md-primary s1-md-bordered"
          @click="setActivePage('manage-user-profile')"
        >configurar agora</md-button>
      </md-dialog-actions>
    </md-dialog>
  </div>
</template>

<script>
import PersonData from "../../data/_person.js";
import Countries from "../../data/_countryCodes.js";
import Languages from "../../data/_languages.js";

export default {
  name: "CreateUserToApp",
  props: {
    setActivePage: Function
  },
  data: () => ({
    person: PersonData,
    countries: Countries,
    languages: Languages,
    workspaceSugestion: null,
    showSugestion: true,
    showPasswordDialog: false,
    showDialogProfileOption: false,
    form: {
      FirstName: "",
      LastName: "",
      Username: "",
      Email: "",
      Password: "",
      ConfirmPassword: "",
      AccountsProfile1: "Normal",
      AccountsProfile2: "Normal",
      AccountsProfile3: "Normal",
      Account: "Icatu MV"
    },
    settings: {
      DNS: null,
      Workspace: null,
      EnabledForgotPassword: true,
      EnabledTwoFactorAuthentication: false
    },
    logoUrl: null,
    showPasswordFeedback: false
  }),
  methods: {
    setShowPasswordDialog() {
      this.showPasswordDialog = true;
      setTimeout(() => {
        document.getElementById("current-password").focus();
      }, 500);
    },
    unsetShowPasswordDialog() {
      this.showPasswordDialog = false;
      this.showPasswordFeedback = true;
    },
    unsetCancelingShowPasswordDialog() {
      this.showPasswordDialog = false;
    },
    logoChanged(files) {
      this.logo = files[0];
      const current = this.logoUrl;

      if (!this.logo) {
        this.logoUrl = current;
        return;
      }

      this.logoUrl = URL.createObjectURL(this.logo);
    },
    uploadImage() {
      document.getElementById("input-upload-image").click();
    },
    getWorkspaceSugestion() {
      this.showSugestion = true;
      this.workspaceSugestion = this.form.NameFantasy
        ? this.form.NameFantasy.toLowerCase()
            .replace(/[|&;$%@"<>()+,\s]/g, "")
            .replace(/[áàâã]/g, "a")
            .replace(/[éèê]/g, "e")
            .replace(/[íï]/g, "i")
            .replace(/[óôõö]/g, "o")
            .replace(/[ú]/g, "u")
            .replace(/[ç]/g, "c")
            .replace(/[ñ]/g, "n")
        : "dominio";
    },
    setWorkspaceSugestion() {
      this.settings.Workspace = this.workspaceSugestion;
    }
  },
  mounted: function() {
    this.$nextTick(function() {
      document.querySelector("input").focus();
    });
  }
};
</script>

