<template>
  <div class="container h-100">
    <div class="row h-100 justify-content-center align-items-center">
      <!--  Sign in  -->
      <form v-show="step === 0"
            class="col-sm-5"
            @submit.prevent="signInUser"
            autocomplete="on"
            novalidate>

<!--        <pre>{{ $v.formSignIn.email}}</pre>-->
        <div v-show="step === 0" class="steps">
          <a class="mb_24 logo" href="/">
            <img alt="Loyverse POS"
                 src="./assets/logo.svg">
          </a>

          <h3 class="sf-instructions">
            {{ signInAccount }}
          </h3>

          <div class="form-group mb_24">
            <label for="s_email">Your email</label>
            <input v-model="formSignIn.email"
                   @blur="$v.formSignIn.email.$touch()"
                   :class="{ 'is-invalid' : $v.formSignIn.email.$error }"
                   type="email"
                   class="form-control"
                   id="s_email"
                   placeholder="exemple@exemple.com">

            <div v-if="!$v.formSignIn.email.required"
                 class="invalid-feedback">
              Input must be not empty
            </div>
            <div v-if="!$v.formSignIn.email.email"
                 class="invalid-feedback">
              {{ emailError }}
            </div>
          </div>

          <div class="form-group mb_48">
            <label for="password">Your password</label>
              <input v-model="formSignIn.password"
                     @blur="$v.formSignIn.password.$touch()"
                     :class="{ 'is-invalid' : $v.formSignIn.password.$error }"
                     type="password"
                     autocomplete="on"
                     class="form-control new-password">

            <div v-if="!$v.formSignIn.password.required"
                 class="invalid-feedback">
              {{ msgRequared }}
            </div>
            <div v-if="!$v.formSignIn.password.minLength"
                 class="invalid-feedback">
              More then 6 symbols
            </div>
          </div>

          <div class="s_btn_block">
            <div class="custom-control custom-checkbox sf-checkbox">
              <input type="checkbox"
                     v-model="s_checked"
                     class="custom-control-input"
                     id="customCheck">
              <label class="custom-control-label" for="customCheck">
                Remember me
              </label>
            </div>
            <button :disabled="!$v.formSignIn.password.required"
                    type="submit"
                    class="btn btn-success sf-submit">
              Sign in
            </button>
          </div>

          <div class="sf-links mt_24">
            <div class="sf-link">
              <a @click="ForgotPassword"
                 href="#"
              >Forgot password?</a>
            </div>
            <div class="sf-link">
              <a @click="registrationStep"
                 href="#"
                 class="sign-in-org" >New to Loyverse?</a>
            </div>
          </div>
        </div>
        <div class="overhead-lang overhead-lang-bottom">
          <div id="overhead-lang-header1" class="overhead-lang-header overhead-lang-header-bottom clearfix">
            <div class="lang-code-bottom">English</div>
            <div class="menu-button"></div>
          </div>
          <ul class="menu menu-bottom">
            <li class="first leaf menu-item-524"><a href="/signin">English</a></li>
            <li class="leaf menu-item-530"><a href="/fr/signin" title="">Français</a></li>
            <li class="leaf menu-item-534"><a href="/ro/signin" title="">Română</a></li>
            <li class="leaf menu-item-540"><a href="/jp/signin" title="">日本語</a></li>
            <li class="leaf menu-item-542"><a href="/gr/signin" title="">Ελληνικά</a></li>
            <li class="leaf menu-item-656"><a href="/de/signin" title="">Deutsch</a></li>
            <li class="leaf menu-item-794"><a href="/es/signin" title="">Español</a></li>
            <li class="leaf menu-item-2545"><a href="/mx/signin" title="">Español(Mx)</a></li>
            <li class="leaf menu-item-703"><a href="/idn/signin" title="">Indonesia</a></li>
            <li class="leaf menu-item-714"><a href="/it/signin" title="">Italiano</a></li>
            <li class="leaf menu-item-1838"><a href="/ms/signin" title="">Malay</a></li>
            <li class="leaf menu-item-695"><a href="/nl/signin" title="">Nederlands</a></li>
            <li class="leaf menu-item-706"><a href="/no/signin" title="">Norsk</a></li>
            <li class="leaf menu-item-792"><a href="/pl/signin" title="">Polski</a></li>
            <li class="leaf menu-item-724"><a href="/br/signin" title="">Português (BR)</a></li>
            <li class="leaf menu-item-699"><a href="/se/signin" title="">Svenska</a></li>
            <li class="leaf menu-item-3026"><a href="/sk/signin" title="">Slovenský</a></li>
            <li class="leaf menu-item-692"><a href="/vn/signin" title="">Tiếng Việt</a></li>
            <li class="leaf menu-item-737"><a href="/tr/signin" title="">Türk</a></li>
            <li class="leaf menu-item-688"><a href="/cz/signin" title="">Čeština</a></li>
            <li class="leaf menu-item-690"><a href="/bg/signin" title="">Български</a></li>
            <li class="leaf menu-item-728"><a href="/ee/signin" title="">Еesti</a></li>
            <li class="leaf menu-item-733"><a href="/mn/signin" title="">Монгол</a></li>
            <li class="leaf menu-item-793"><a href="/ru/signin" title="">Русский</a></li>
            <li class="leaf menu-item-1850"><a href="/ar/signin" title="">العربية</a></li>
            <li class="leaf menu-item-709"><a href="/th/signin" title="">ภาษาไทย</a></li>
            <li class="leaf menu-item-740"><a href="/ge/signin" title="">ქართული</a></li>
            <li class="leaf menu-item-3011"><a href="/zh/signin">中文 (繁體)</a></li>
            <li class="leaf menu-item-720"><a href="/cn/signin">中文 (简体)</a></li>
            <li class="last leaf menu-item-718"><a href="/ko/signin" title="">한국어</a></li>
          </ul>
        </div>
      </form>
      <!--  END Sign in  -->


      <!--  Create your free Loyverse account  -->
      <form class="col-sm-5"
            v-show="step === 1 || step === 2 || step === 3 || step === 4"
            @submit.prevent="registerUser"
            autocomplete="on"
            novalidate>
<!--        <transition name="fadedd" mode="out-in">-->
          <div v-if="step === 1" class="steps">
              <a class="mb_24 logo" href="/">
                <img alt="Loyverse POS"
                     src="./assets/logo.svg">
              </a>
              <h3 class="mb_24 sf-instructions">
                {{ createAccount }}
              </h3>

              <div class="form-group">
                <label for="email">Your email</label>
                <input v-model="formReg.email"
                       @blur="$v.formReg.email.$touch()"
                       :class="status($v.formReg.email)"
                       type="email"
                       class="form-control"
                       id="email"
                       placeholder="Exemple@exemple.com">

                <div v-if="!$v.formReg.email.required"
                     class="invalid-feedback">
                  Input must be not empty
                </div>
                <div v-if="!$v.formReg.email.email"
                     class="invalid-feedback">
                  {{ emailError }}
                </div>
              </div>

              <div class="btn_block">
                <button @click="nextStep"
                        :disabled="disabledButton1"
                        type="button"
                        class="btn btn-success">Next step</button>
              </div>
              <p class="mt_24 smalltext">
                Already have an account?
                <a class="signinfromsignup"
                   @click="signInStep"
                   href="#">
                  Sign in</a>
              </p>
            </div>
          <div v-else-if="step === 2" class="steps">
          <a class="mb_24 logo" href="/">
            <img alt="Loyverse POS"
                 src="./assets/logo.svg">
          </a>
          <h3 class="mb_24 sf-instructions">
            {{ createAccount }}
          </h3>
          <div class="form-group">
            <label for="password">Your password</label>

            <input v-model="formReg.password"
                   @blur="$v.formReg.password.$touch()"
                   :class="status($v.formReg.password)"
                   type="password"
                   autocomplete="off"
                   class="form-control new-password"
                   id="password">
            <div v-if="!$v.formReg.password.required"
                 class="invalid-feedback">
              {{ msgRequared }}
            </div>
            <div v-if="!$v.formReg.password.minLength"
                 class="invalid-feedback">
              More then 6 symbols
            </div>
          </div>



          <div class="form-group">
            <label for="passwordConfirm">Confirm password</label>
            <input v-model="formReg.passwordConfirm"
                   @blur="$v.formReg.passwordConfirm.$touch()"
                   :class="status($v.formReg.passwordConfirm)"
                   type="password"
                   class="form-control new-password"
                   autocomplete="off"
                   id="passwordConfirm">
            <div v-if="!$v.formReg.passwordConfirm.sameAs"
                 class="invalid-feedback">
              Passwords don't fall out!
            </div>
          </div>


          <div class="btn_block">
            <button @click="backStep"
                    type="button"
                    class="mr-2 btn btn-light">Back</button>
            <button @click="nextStep"
                    type="button"
                    :disabled="disabledButton2"
                    class="btn btn-success">Next step</button>
          </div>

          <p class="mt_24 smalltext">
            Already have an account?
            <a class="signinfromsignup"
               @click="signInStep"
               href="#">
              Sign in</a>
          </p>
        </div>
          <div v-else-if="step === 3" class="steps ">
            <a class="mb_24 logo" href="/">
              <img alt="Loyverse POS"
                   src="./assets/logo.svg">
            </a>
            <h3 class="mb_24 sf-instructions">
              {{ createAccount }}
            </h3>

            <div class="form-group">
              <label for="name">Business name</label>

              <input v-model="formReg.name"
                     @blur="$v.formReg.name.$touch()"
                     :class="status($v.formReg.name)"
                     type="text"
                     class="form-control"
                     id="name"
                     placeholder="John Smith">
              <div v-if="$v.formReg.name.minLength" class="invalid-feedback">
                Need more symbols...
              </div>
              <div v-if="$v.formReg.name.required" class="invalid-feedback">
                Please enter your name.
              </div>
            </div>
            <div class="btn_block">
              <button @click="backStep"
                      type="button"
                      class="mr-2 btn btn-light">Back</button>
              <button @click="nextStep"
                      :disabled="disabledButton3"
                      type="button"
                      class="btn btn-success">Next step</button>
            </div>
            <p class="mt_24 smalltext">
              Already have an account?
              <a class="signinfromsignup"
                 @click="signInStep"
                 href="#">
                Sign in</a>
            </p>
          </div>
          <div v-else-if="step === 4" class="steps">
            <a class="mb_24 logo" href="/">
              <img alt="Loyverse POS"
                   src="./assets/logo.svg">
            </a>
            <h3 class="mb_24 sf-instructions">
              {{ createAccount }}
            </h3>

            <div class="form-group">
              <label for="country">Select your country</label>
              <select class="custom-select rf-textinput"
                      v-model="formReg.country"
                      id="country">
                <option disabled value="">Chose from list</option>
                <option value="AF">Afghanistan</option>
                <option value="AX">Åland Islands</option>
                <option value="AL">Albania</option>
                <option value="DZ">Algeria</option>
                <option value="AS">American Samoa</option>
                <option value="AD">Andorra</option>
                <option value="AO">Angola</option><option value="AI">Anguilla</option><option value="AG">Antigua &amp; Barbuda</option><option value="AR">Argentina</option><option value="AM">Armenia</option><option value="AW">Aruba</option><option value="AU">Australia</option><option value="AT">Austria</option><option value="AZ">Azerbaijan</option><option value="BS">Bahamas</option><option value="BH">Bahrain</option><option value="BD">Bangladesh</option><option value="BB">Barbados</option><option value="BY">Belarus</option><option value="BE">Belgium</option><option value="BZ">Belize</option><option value="BJ">Benin</option><option value="BM">Bermuda</option><option value="BT">Bhutan</option><option value="BO">Bolivia</option><option value="BA">Bosnia &amp; Herzegovina</option><option value="BW">Botswana</option><option value="BV">Bouvet Island</option><option value="BR">Brazil</option><option value="IO">British Indian Ocean Territory</option><option value="VG">British Virgin Islands</option><option value="BN">Brunei</option><option value="BG">Bulgaria</option><option value="BF">Burkina Faso</option><option value="BI">Burundi</option><option value="KH">Cambodia</option><option value="CM">Cameroon</option><option value="CA">Canada</option><option value="CV">Cape Verde</option><option value="KY">Cayman Islands</option><option value="CF">Central African Republic</option><option value="TD">Chad</option><option value="CL">Chile</option><option value="CN">China</option><option value="CX">Christmas Island</option><option value="CC">Cocos (Keeling) Islands</option><option value="CO">Colombia</option><option value="KM">Comoros</option><option value="CG">Congo - Brazzaville</option><option value="CD">Congo - Kinshasa</option><option value="CK">Cook Islands</option><option value="CR">Costa Rica</option><option value="CI">Côte d’Ivoire</option><option value="HR">Croatia</option><option value="CU">Cuba</option><option value="CW">Curaçao</option><option value="CY">Cyprus</option><option value="CZ">Czech Republic</option><option value="DK">Denmark</option><option value="DJ">Djibouti</option><option value="DM">Dominica</option><option value="DO">Dominican Republic</option><option value="EC">Ecuador</option><option value="EG">Egypt</option><option value="SV">El Salvador</option><option value="GQ">Equatorial Guinea</option><option value="ER">Eritrea</option><option value="EE">Estonia</option><option value="SZ">Eswatini</option><option value="ET">Ethiopia</option><option value="FK">Falkland Islands</option><option value="FO">Faroe Islands</option><option value="FJ">Fiji</option><option value="FI">Finland</option><option value="FR">France</option><option value="GF">French Guiana</option><option value="PF">French Polynesia</option><option value="GA">Gabon</option><option value="GM">Gambia</option><option value="GE">Georgia</option><option value="DE">Germany</option><option value="GH">Ghana</option><option value="GI">Gibraltar</option><option value="GR">Greece</option><option value="GL">Greenland</option><option value="GD">Grenada</option><option value="GP">Guadeloupe</option><option value="GU">Guam</option><option value="GT">Guatemala</option><option value="GG">Guernsey</option><option value="GN">Guinea</option><option value="GW">Guinea-Bissau</option><option value="GY">Guyana</option><option value="HT">Haiti</option><option value="HM">Heard &amp; McDonald Islands</option><option value="HN">Honduras</option><option value="HK">Hong Kong SAR China</option><option value="HU">Hungary</option><option value="IS">Iceland</option><option value="IN">India</option><option value="ID">Indonesia</option><option value="IR">Iran</option><option value="IQ">Iraq</option><option value="IE">Ireland</option><option value="IM">Isle of Man</option><option value="IL">Israel</option><option value="IT">Italy</option><option value="JM">Jamaica</option><option value="JP">Japan</option><option value="JE">Jersey</option><option value="JO">Jordan</option><option value="KZ">Kazakhstan</option><option value="KE">Kenya</option><option value="KI">Kiribati</option><option value="KW">Kuwait</option><option value="KG">Kyrgyzstan</option><option value="LA">Laos</option><option value="LV">Latvia</option><option value="LB">Lebanon</option><option value="LS">Lesotho</option><option value="LR">Liberia</option><option value="LY">Libya</option><option value="LI">Liechtenstein</option><option value="LT">Lithuania</option><option value="LU">Luxembourg</option><option value="MO">Macao SAR China</option><option value="MG">Madagascar</option><option value="MW">Malawi</option><option value="MY">Malaysia</option><option value="MV">Maldives</option><option value="ML">Mali</option><option value="MT">Malta</option><option value="MH">Marshall Islands</option><option value="MQ">Martinique</option><option value="MR">Mauritania</option><option value="MU">Mauritius</option><option value="YT">Mayotte</option><option value="MX">Mexico</option><option value="FM">Micronesia</option><option value="MD">Moldova</option><option value="MC">Monaco</option><option value="MN">Mongolia</option><option value="ME">Montenegro</option><option value="MS">Montserrat</option><option value="MA">Morocco</option><option value="MZ">Mozambique</option><option value="MM">Myanmar (Burma)</option><option value="NA">Namibia</option><option value="NR">Nauru</option><option value="NP">Nepal</option><option value="NL">Netherlands</option><option value="NC">New Caledonia</option><option value="NZ">New Zealand</option><option value="NI">Nicaragua</option><option value="NE">Niger</option><option value="NG">Nigeria</option><option value="NU">Niue</option><option value="NF">Norfolk Island</option><option value="MK">North Macedonia</option><option value="MP">Northern Mariana Islands</option><option value="NO">Norway</option><option value="OM">Oman</option><option value="PK">Pakistan</option><option value="PW">Palau</option><option value="PS">Palestinian Territories</option><option value="PA">Panama</option><option value="PG">Papua New Guinea</option><option value="PY">Paraguay</option><option value="PE">Peru</option><option value="PH">Philippines</option><option value="PN">Pitcairn Islands</option><option value="PL">Poland</option><option value="PT">Portugal</option><option value="PR">Puerto Rico</option><option value="QA">Qatar</option><option value="RE">Réunion</option><option value="RO">Romania</option><option value="RU">Russia</option><option value="RW">Rwanda</option><option value="WS">Samoa</option><option value="SM">San Marino</option><option value="ST">São Tomé &amp; Príncipe</option><option value="SA">Saudi Arabia</option><option value="SN">Senegal</option><option value="RS">Serbia</option><option value="SC">Seychelles</option><option value="SL">Sierra Leone</option><option value="SG">Singapore</option><option value="SX">Sint Maarten</option><option value="SK">Slovakia</option><option value="SI">Slovenia</option><option value="SB">Solomon Islands</option><option value="SO">Somalia</option><option value="ZA">South Africa</option><option value="KR">South Korea</option><option value="SS">South Sudan</option><option value="ES">Spain</option><option value="LK">Sri Lanka</option><option value="BL">St. Barthélemy</option><option value="SH">St. Helena</option><option value="KN">St. Kitts &amp; Nevis</option><option value="LC">St. Lucia</option><option value="MF">St. Martin</option><option value="PM">St. Pierre &amp; Miquelon</option><option value="VC">St. Vincent &amp; Grenadines</option><option value="SD">Sudan</option><option value="SR">Suriname</option><option value="SJ">Svalbard &amp; Jan Mayen</option><option value="SE">Sweden</option><option value="CH">Switzerland</option><option value="SY">Syria</option><option value="TW">Taiwan</option><option value="TJ">Tajikistan</option><option value="TZ">Tanzania</option><option value="TH">Thailand</option><option value="TL">Timor-Leste</option><option value="TG">Togo</option><option value="TK">Tokelau</option><option value="TO">Tonga</option><option value="TT">Trinidad &amp; Tobago</option><option value="TN">Tunisia</option><option value="TR">Turkey</option><option value="TM">Turkmenistan</option><option value="TC">Turks &amp; Caicos Islands</option><option value="TV">Tuvalu</option><option value="UM">U.S. Outlying Islands</option><option value="VI">U.S. Virgin Islands</option><option value="UG">Uganda</option><option value="UA">Ukraine</option><option value="AE">United Arab Emirates</option><option value="GB">United Kingdom</option><option value="US">United States</option><option value="UY">Uruguay</option><option value="UZ">Uzbekistan</option><option value="VU">Vanuatu</option><option value="VE">Venezuela</option><option value="VN">Vietnam</option><option value="WF">Wallis &amp; Futuna</option><option value="EH">Western Sahara</option><option value="YE">Yemen</option><option value="ZM">Zambia</option><option value="ZW">Zimbabwe</option>
              </select>
            </div>

            <div class="custom-control custom-checkbox">
              <input type="checkbox"
                     v-model="checked"
                     class="custom-control-input"
                     id="customCheck1">
              <label class="rf-smalltext custom-control-label"
                     for="customCheck1"
                     id="privacy"
                     style="text-align: left;">
                I agree to Loyverse
                <a href="https://loyverse.com/terms-use"
                   target="_blank">
                  Terms of Use
                </a>
                and have read and acknowledged
                <a href="https://loyverse.com/privacy-policy"
                   target="_blank">Privacy Policy
                </a>
              </label>
            </div>

            <div class="btn_block">
              <button @click="backStep"
                      type="button"
                      class="mr-2 btn btn-light">Back</button>
              <button type="submit"
                      :disabled="!disableRegistred"
                      class="btn btn-success">Sign up</button>
            </div>

            <p class="mt_24 smalltext">
              Already have an account?
              <a class="signinfromsignup"
                 @click="signInStep">
                Sign in</a>
            </p>

          </div>
<!--        </transition>-->


        <!--  Progress Bar  -->
        <div v-show="step === 1"
             class="progress">
          <div class="progress-bar bg-success" role="progressbar" aria-valuenow="25"
               aria-valuemin="0" aria-valuemax="100" style="width:25%">
<!--            40% Complete (success)-->
          </div>
        </div>
        <div v-show="step === 2"
             class="progress">
          <div class="progress-bar bg-success" role="progressbar" aria-valuenow="50"
               aria-valuemin="0" aria-valuemax="100" style="width:50%">
<!--            40% Complete (success)-->
          </div>
        </div>
        <div v-show="step === 3"
             class="progress">
          <div class="progress-bar bg-success" role="progressbar" aria-valuenow="75"
               aria-valuemin="0" aria-valuemax="100" style="width:75%">
<!--            40% Complete (success)-->
          </div>
        </div>
        <div v-show="step === 4"
             class="progress">
          <div class="progress-bar bg-success" role="progressbar" aria-valuenow="100"
               aria-valuemin="0" aria-valuemax="100" style="width:100%">
<!--            40% Complete (success)-->
          </div>
        </div>
        <!--  END Progress Bar  -->
      </form>
      <!--  END Create your free Loyverse account  -->


      <!--  Reset password  -->
      <form v-show="step === 5"
            class="col-sm-5"
            @submit.prevent="ForgotPasswordUser"
            autocomplete="on"
            novalidate>
        <div v-show="step === 5" class="steps">
          <a class="mb_24 logo" href="/">
            <img alt="Loyverse POS"
                 src="./assets/logo.svg">
          </a>
          <h1 class="pb_0 sf-instructions">Reset password</h1>
          <h3 class="sf-instructions">
            Enter your email address to receive instructions
            to reset your password
          </h3>

          <div class="form-group mb_48">
            <label for="r_email">Enter your email</label>
            <input v-model="formRestorePassword.email"
                   @blur="$v.formRestorePassword.email.$touch()"
                   :class="{ 'is-invalid' : $v.formRestorePassword.email.$error }"
                   type="email"
                   class="form-control"
                   id="r_email"
                   placeholder="Exemple@exemple.com">

            <div v-if="!$v.formRestorePassword.email.required"
                 class="invalid-feedback">
              Input must be not empty
            </div>
            <div v-if="!$v.formRestorePassword.email.email"
                 class="invalid-feedback">
              {{ emailError }}
            </div>
          </div>

          <button :disabled="!$v.formRestorePassword.email.required"
                  type="submit"
                  class="btn btn-success sf-submit">Send
          </button>
          <div class="sf-link">
            <a @click="signInStep"
               href="#">Back to Sign in form</a>
          </div>
        </div>
      </form>
      <!--  END Reset password  -->

    </div>

  </div>
</template>

<script>
import { required, email, minLength, sameAs, alpha} from 'vuelidate/lib/validators'

export default {
  data() {
    return {
      step: 0,
      formSignIn: {
        email: '',
        password: '',
      },
      formReg: {
        email: '',
        password: '',
        passwordConfirm: '',
        name: '',
        country: '',
      },
      formRestorePassword: {
        email: '',
      },
      signInAccount: "Sign in to your Loyverse account",
      createAccount: "Create your free Loyverse account",
      msgRequared: "Input must be not empty",
      emailError: "It doesn't match the pattern xxxx@xx.xx",
      checked: false,
      s_checked: true,
    }
  },
  methods: {
    status(validator) {
       return {
         'is-invalid': validator.$error,
       }
    },
    nextStep() {
      if (this.step < 4) {
        this.step++
      }
    },
    backStep() {
      if (this.step > 1) {
        this.step--
      }
    },

    signInStep() {
      this.step = 0
    },
    signInUser() {
      console.log("Success signIn")
      console.log(this.formSignIn)
    },

    ForgotPassword() {
      this.step = 5
    },
    ForgotPasswordUser() {
      console.log(this.formRestorePassword)
    },

    registrationStep() {
      this.step = 1
    },
    registerUser() {
      console.log("Success registration")
      console.log(this.formReg)
      // window.open('https://drupal8.loyverse.com/', '_blank');

      this.step = 1

      for (let input in this.formReg) {
        this.formReg[input] = ''
      }

      this.$v.$reset()



    },
  },
  computed: {
    disabledButton1() {
      return this.$v.formReg.email.$invalid
    },
    disabledButton2() {
      return this.$v.formReg.password.$invalid ||
          this.$v.formReg.passwordConfirm.$invalid
    },
    disabledButton3() {
      return this.$v.formReg.name.$invalid
    },
    disableRegistred() {
      return this.checked
    }
  },
  validations: {
    formReg: {
      email: {
        required,
        email,
      },
      password: {
        required,
        minLength: minLength(6)
      },
      passwordConfirm: {
        sameAs: sameAs('password')
      },
      name: {
        required,
      },
      country: {
        alpha,
      },
    },
    formSignIn: {
      email: {
        required,
        email,
      },
      password: {
        required,
        minLength: minLength(6)
      },
    },
    formRestorePassword: {
      email: {
        required,
        email,
      },
    },
  }
}
</script>

<style>
body {
  background-color: #f2f2f2;
  height: 100vh;
}
.logo {
  display: block;
}
.custom-select:focus,
.form-control:focus {
  border-color: #28a745;
  box-shadow: 0 0 0 0.2rem rgba(40, 167, 69, 0.25);
}
.was-validated .form-control:invalid {
  background-color: #fae8eb;
}
.steps {
  background-color: white;
  padding: 24px;
  box-shadow: 0 1px 4px 0 rgba(0,0,0,0.14);
}
label {
  font-size: 0.75rem;
}
.custom-control-label {
  font-size: 1rem;
}
.btn {
  text-transform: uppercase;
  padding: .5rem 1rem;
}
.btn-success {
  width: 100%;
  background: #8bc34a;
}
.btn-success:focus,
.btn-success:hover {
  background: #689F38;
}
.btn-success:disabled {
  color: #fff;
  background: #8bc34a;
  border-color: #28a745;
}
.btn_block {
  display: flex;
  justify-content: flex-end;
  margin-top: 64px;
}
.s_btn_block {
  display: flex;
  align-items: center;
  justify-content: space-between;
}
.s_btn_block .btn-success{
  width: auto;
}
.sf-link {
  padding-top: 8px;
  font-size: 14px;
}
.sf-instructions {
  padding-bottom: 40px;
  font-size: 18px;
  font-weight: 400;
}
.pb_0 {
  padding-bottom: 0;
}
.mb_24 {
  margin-bottom: 24px;
}
.mb_48 {
  margin-bottom: 48px;
}
.mt_24 {
  margin-top: 24px;
}
.smalltext {
  color: #757575;
  color: rgba(0, 0, 0, .54);
  font-size: 12px;
  text-align: center;
  padding: 0;
}


.fadedd-enter-active,
.fadedd-leave-active {
  transition: opacity 0.8s;
}
.fadedd-enter,
.fadedd-leave-to /* .fade-leave-active до версии 2.1.8 */ {
  opacity: 0;
}


.progress {
  height: 0.5rem;
  border: 1px solid darkgrey;
}

.overhead-lang,
.overhead-products {
  float: right;
  position: relative;
  height: 24px;
  z-index: 1000;
}
.overhead-lang-bottom {
  float: left;
}
.overhead-lang-header {
  padding: 0 8px;
  cursor: pointer;
  border-left-width: 1px;
  border-left-style: solid;
  border-left-color: transparent;
  border-right-width: 1px;
  border-right-style: solid;
  border-right-color: transparent;
}

.overhead-lang-header-bottom {
  height: 0;
  padding: 0;
  width: 160px;
  float: left;
}
.lang-code-bottom {
  float: inherit;
  margin: 16px 0 0 0;
  text-transform: none;
  font-weight: 400;
  font-size: 12px;
  position: relative;
  padding-right: 16px;
}
.lang-code-bottom:after {
  content: "";
  display: block;
  position: absolute;
  width: 0;
  height: 0;
  border-style: solid;
  border-width: 5px 5px 0 5px;
  border-color: #212121 transparent transparent transparent;
  top: 7px;
  right: 0;
}
.overhead-lang .menu-button {
  width: 17px;
  height: 24px;
  top: 0;
  right: 0;
  cursor: pointer;
  float: right;
  margin: 0 8px 0 0;
  -webkit-box-sizing: border-box;
  -moz-box-sizing: border-box;
  box-sizing: border-box;
}
.overhead-lang .menu {
  position: absolute;
  top: 24px;
  right: -1px;
  z-index: 1000;
  display: none;
  width: 300px;
  -webkit-box-sizing: border-box;
  -moz-box-sizing: border-box;
  box-sizing: border-box;
  padding: 5px 0;
  font-size: 0;
  text-align: left;
  list-style: none;
  background-color: #fff;
  /*border: 1px solid #ccc;*/
  border: 1px solid rgba(0, 0, 0, .15);
  border-top: none;
  border-radius: 0 0 4px 4px;
}
.overhead-lang .menu-bottom {
  display: block;
  height: 316px;
  width: 160px;
  top: -316px;
  overflow-y: auto;
  overflow-x: hidden;
  right: 0;
  -webkit-box-shadow: 0 8px 10px 1px rgba(0,0,0,0.14), 0 3px 14px 2px rgba(0,0,0,0.12), 0 5px 5px -3px rgba(0,0,0,0.2);
  box-shadow: 0 8px 10px 1px rgba(0,0,0,0.14), 0 3px 14px 2px rgba(0,0,0,0.12), 0 5px 5px -3px rgba(0,0,0,0.2);
  border: 1px solid rgba(0, 0, 0, .15);
  font-size: 24px;
}
.overhead-lang .menu-bottom {
  display: none;
}
.overhead-lang .menu li {
  list-style: none;
  margin: 5px 0 0;
  padding: 0;
  width: 50%;
  display: inline-block;
  font-size: 14px;
}
.overhead-lang .menu-bottom li {
  margin: 8px 0;
  width: 100%;
}
.overhead-lang .menu > li > a {
  padding: 3px 20px;
  font-weight: normal;
  line-height: 1.42857143;
  color: #333;
  white-space: nowrap;
}
.overhead-lang .menu-bottom > li > a {
  padding: 9px 100px 9px 20px;
  font-weight: 400;
  font-size: 12px;
}
.overhead-lang .menu > li > a:hover,
.overhead-lang .menu > li > a:focus {
  color: #262626;
  text-decoration: none;
  background-color: #f5f5f5;
}
</style>
