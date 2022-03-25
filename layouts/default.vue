<template>
<section>
  <section id="visual">
    <div class="visual_blur_box">
        <div class="ex_poster"></div>
        <h2 class="visual_tit">Impressionism</h2>
    </div>
  </section>
  <section id="nav" :class="{'fixed_nav' : !scrollVisual}">
    <ul>
      <li><a href="#visual">Exhibition Info</a></li>
      <li><a href="#artists_info">Artists</a></li>
      <li><a href="#gallery">Gallery</a></li>
    </ul>
  </section>
  <section id="exhibition_info">
    <h2 class="sec_tit">Exhibition Info</h2>
    <div class="center">
      <div class="ex_info">
        <h3 class="title">Impressionism</h3>
        <p class="sub_tit">1865 -</p>
        <div class="link_box">
          <ul>
            <li><a href="#void"><img src="../assets/icon_01_phone.png" alt="phone"></a></li>
            <li><a href="#void"><img src="../assets/icon_02_email.png" alt="emial"></a></li>
            <li><a href="#void"><img src="../assets/icon_03_insta.png" alt="instagram"></a></li>
            <li><a href="#void"><img src="../assets/icon_04_facebook.png" alt="facebook"></a></li>
            <li><a href="#void"><img src="../assets/icon_05_link.png" alt="link"></a></li>
          </ul>
        </div>
        <p class="cont_txt">Term generally applied to a movement in art in France in the late 19th century.<br/> The movement gave rise to such ancillaries as American Impressionism. The primary use of the term Impressionist is for a group of French painters who worked between around 1860 and 1900, especially to describe their works of the later 1860s to mid-1880s. These artists include Frédéric Bazille, Paul Cézanne, Edgar Degas, Edouard Manet, Claude Monet, Berthe Morisot, Camille Pissarro, Auguste Renoir and Alfred Sisley, as well as Mary Cassatt, Gustave Caillebotte (who was also an important early collector), Eva Gonzalès, Armand Guillaumin and Stanislas Lépine. The movement was anti-academic in its formal aspects and involved the establishment of venues other than the official Salon for showing and selling paintings.</p>
        <b-button type="is-dark" >3D 전시 보기</b-button>
      </div>
    </div>
  </section>
  <section id="artists_info">
    <div class="center">
      <h2 class="sec_tit">Artists</h2>
      <b-carousel-list class="artist_slide" v-model="test" :data="items" :items-to-show="5">
        <template #item="list">
            <div class="card">
                <div class="card-image">
                    <figure class="image is-5by4">
                        <a><img :src="list.image"></a>
                    </figure>
                </div>
                <div class="card-content">
                    <div class="content">
                        <p class="title is-6" style="margin-bottom:0;">{{ list.title }}</p>
                        <ul class="artist_link">
                            <li><a href="#void"><img src="../assets/icon_01_phone.png" alt="phone" ></a></li>
                            <li><a href="#void"><img src="../assets/icon_02_email.png" alt="emial" ></a></li>
                            <li><a href="#void"><img src="../assets/icon_03_insta.png" alt="instagram" ></a></li>
                            <li><a href="#void"><img src="../assets/icon_04_facebook.png" alt="facebook" ></a></li>
                            <li><a href="#void"><img src="../assets/icon_05_link.png" alt="link" ></a></li>
                        </ul>
                    </div>
                </div>
            </div>
        </template>
    </b-carousel-list>
    </div>
  </section>
  <section id="gallery">
    <div class="center">
      <h2 class="sec_tit">Exhibition Info</h2>
      <h3 class="title">Gallery</h3>
      <ul>
        <li v-for="(artList,i) in arts" :key="i" :style="{ backgroundImage: 'url(' + artList.images + ')' }">
          <a href="#void" @click="[isCardModalActive = true,modalData(artList.images,artList.title,artList.artist,artList.info)]">
            <h4>{{artList.title}}</h4>
            <p>{{artList.artist}}</p>
          </a>
        </li>
      </ul>
      <b-modal v-model="isCardModalActive" :width="640">
            <div class="card">
                <div class="card-image">
                    <figure class="image is-4by3 modal_img" :style="{ backgroundImage: 'url(' + imageData + ')' }">
                    </figure>
                </div>
                <div class="card-content">
                    <div class="media">
                        <div class="media-content">
                            <h3 class="modal_tit">{{titleData}}</h3>
                            <h6 class="modal_artist">{{artistData}}</h6>
                            <p class="modal_info">{{infoData}}</p>
                        </div>
                    </div>
                </div>
            </div>
        </b-modal>
    </div>
  </section>
  <footer>
    <div class="center">
      <img src="../assets/360xcon_f_logo.png" alt="360xcon">
      <ul>
        <li><a href="#void">서비스 약관</a></li>
        <li><a href="#void">개인정보 보호정책</a></li>
        <li>Copyright dataking.Inc 2021 All rights reserved.</li>
      </ul>
    </div>
  </footer>
  </section>
</template>
<script>
export default {
  name: 'DefaultLayout',
  mounted(){
    window.addEventListener('scroll', this.onScroll)
  },
  beforeDestroy(){ 
    window.removeEventListener('scroll', this.onScroll) 
  },
  methods:{
    info(value) {
      this.test = value
    },
    modalData(data1,data2,data3,data4){
      this.imageData = data1;
      this.titleData = data2;
      this.artistData = data3;
      this.infoData = data4;
    },
    onScroll(){
      const currentScrollPosition = window.pageYOffset || document.documentElement.scrollTop
      if (currentScrollPosition < 0) { return }
      if (Math.abs(currentScrollPosition - this.lastScrollPosition) < 380) { return }
      this.scrollVisual = currentScrollPosition < this.lastScrollPosition
      this.lastScrollPosition = currentScrollPosition
    }
  },
  data () {
    return {
            test: 0,
            isCardModalActive: false,
            imageData:{},
            titleData:{},
            artistData:{},
            infoData:{},
            scrollVisual: true,
            lastScrollPosition: 0,
            items: [
                {
                    title: 'Vincent Van Gogh',
                    image: 'https://lh3.googleusercontent.com/fife/AAWUweXhLvIAf_exDFZjGaEu74gHWWYjky4va-bMjjS8cJ23WUtiQ82Np5ECtN8KbSOu19JI_Oh6TFIaTUawa091EGqS44TYK3SLVEh6-R5rjzr99-JGm8HO7fMnajYG2FcYJTr1zA7EXMo2wG2CmFAwedW6rroPGWv2pm2jKzU79TzWNs0updgjtSdNpSKv-QV7ixZxNpDVOpVZYNmfUVgwiL_AdlA__GnhRpseAFa4yomtZjocyP1oJ73MGwxfgZVcG9MrsIfxpcIkHBameMx2CHGuyHc1Mc_ZCJThxogIhxCky7fvsJ9Jv8QgN83RvA37-4jkoW7gec_ZZvZBPAYODvfOE03dJpW_bxaCeqqw8pTVQaBYq4-qgxhe-K-2NgEKswrwEyBWbZUKAzG3Q1frUtApuPUnWfdzunGB2EQkWaXHY0-cv0DiIufKBWPNCmagcL41KcfKTkP85gzCPesuuNbRS3u6gHPg3jnawarRvLl3xbw2-kfukV7-X0eDfBe8QrtWvvVBbJogOb2VIxdOsa__WBziWNHPI3j-yS2bbtnJ6l69eK9TpQKj8HebkAdJyjX4HcL_7N-8iezdj4UERCHi4lf-9WxeZig_TxEWOudAqco2GZvXmUrwzfZTIxCsM9Bj-bwouMe7hT9Nny_u-KL0POyja3ZfHrwPXg8wCnmna7mZyU9axAx0HWh0XEacvluC4-L5agXktCc-2RcQN5yLtGQI3fiCgg=w320-h200-k',
                    info: 'aaaaaaa'
                },
                {
                    title: 'Camille Pissarro',
                    image: 'https://lh3.googleusercontent.com/fife/AAWUweWqMH52dVcYrx8D1MXtSl_95gPu25yIqP1L9NSV42QAIwzW0h2JjSSK8hXLtArckYLplmLNqIVDkkfYkDfgkc1aFSV0mNw4OeCHF4nZDZz-29TRaptzW5qny1sihlqCuSg0EX1NFnTO7OyvsYjPJKuvhi8O8S8p7tOINuyybZn6ZIL7g_p_P4qjJrZusTDuZRBJH6fyQOlMXl4cdp-0jNUe2o_EhER_aQDEqE-lP1N_52-_z_FWpr_PqbLbMoh3kqxq4UzFDlDqOIV3OG574UHP97oJwgpk4Mzrt48AojC41imlQazMZ2ILdRM9Gda7FuQCZUWyjeEZCbIX2rklYxBr0kS4lYAHHZ0E4GFv090IlHo6kGV0KlIlykoP1QOpWz7oFZ17zwxlfdo98T05AvvoXGC8A5ChSK-kI91OtN9aT4zD2d1Dqya5Ff7pv0DD2DM9-J1D9oKHBAtQYeY4PQ1M-OvyoyxYqhUzdq_dVqdx0FbDBqqKUvLdHBUJuvw-xQXJbXd2F5Pe2Eek5gsx0ZVZZRBKwVnur29w1DSA_MgkvCj-sh3jBI0cvORptvLaxyHg4AgfGIqo3-nsbPEASxFKEVsq8Zu5-eTxDHM4Cxk8MNtZXGuBwc2sa89EpznOUPlXAQLtbXWbWw8Qejb_LFm68ysL3GfmCUFfQM7wgDHr23gr5xRcsa_Ljk_6yuYmG6JO2jWi6yK_YLxPJjob3nuYD2E4E6P-Eg=w320-h200-k',
                    info: 'bbbbbbb'
                },
                {
                    title: 'Édouard Manet',
                    image: 'https://lh3.googleusercontent.com/fife/AAWUweX0WMY6XcaZw7ntxNhou2IBZbPWh5DYBp44SHFvXsOH7Uu6H65Af6wf-GWxJ28BxgzgNsYRtVchW6MqJf3YAH4s57Q7SEmmZNvB-66eCl_yRzDtlJCaStfEWzQYXmf0to3CYv4H01cyp7M8RoXcc4142q1cGgo9Appi99a23-qN3_T_X09KzJXPx4pqsvEpsfLkX8lkzqUUF0BtjkDdKZYlXLQxcl9wbCYmZHx-ndQW_4lBEV6qR5Bujtrg0n0_CHMqcNEViU9r1jPIdT8ePREjlIUfmhZVvKqkVXVe1duOkcm4obmFBqDErUQux5gwNi1iQ5lcbRtjDwC3CDEf3qO79f09bHIEoVt078Z8_2BklOGDxtFSJuGrugfSqmoUn3CaXH88NeqM89NL6deDBphjhREVCQmh5ihHNomlFhyWf6jWripqIRWR-OoEqdNvPANrAMK3SqyyFd02jBKbAntt3aPz8u1VF2BkPlhTYKNCADbc6xBDTQBEEOZrbCfH1r-DPenV06WAemlxnlzJHWs8zVTsJOsrhUCi90N2yQyuTECPMxHHuz8pPFO33YMPijTGccSWs-SW0qzfeYZjUB1Pt40VSPGsqV0yrbjdGO9cFWlLIm7duMS3aCt402h94xKSoV8CMW75A1CKZaHjnWVgwe6RFrfJcvt34zynqorHMBNqdrVxWRWu7Myl_QAaHJ-_W5xCn1Yk-gLOj5t9gX4GfCI8pkGETw=w320-h200-k',
                    info: 'cccc'
                },
                {
                    title: 'Paul Cézanne',
                    image: 'https://lh3.googleusercontent.com/fife/AAWUweUXgu75cskdZ-LZAPny2dbDhx0z6iRrJYv-47XzDmz9SMInOsASDBmgu1WFXyY5Xut7UXOFl88jDitaErDHZnh-1k3uT44jfESVPdZqbgOxYHo7dO3NVHk0c9jfL5EKyPCTd-qXVN3Pd1UxowcSkzKYGuDCAqDa9-nbVe-vi4dYqh2tb9abouMfNo1exccStnTnw9r6P_BD0hFkZQIs7l3VeV1iCYaKie6lEw8wKy1bPBp_oS9ZidP8gxfze1Itj_U-OzhiCVYsoBzgCILMO0afSl04fe94ao63WHfIdfIdVvp38ux2uYN9jgB5b7hYxXsH-DKpg68a5MSYIdtD6jtnpzXV-lp6Gq9HZjqGeLwcF5PhZJ062r0JCUVcv_xSzpgyk2Z51b5oYhX7Em4Y5kYUifhWdCa6RKV6zzi2aEo_1c5J7-f6bxfYwgJKSekz37FhaKpO4_vWYCqqPQUYQGI4FgpUV9I17vsnmn1ND5Mp9umzPxU6LCFWf3XB-dxmznEoMUqo1WvP9HcQfllWOfJGqncPtDQLmYTG67F6r-9xVZPXH48KLnOVUDNTdYdZF3g4Ghwsn8Mk62BNI3DoTG19Tw2_60jBKuvLuCQ2GxA0k807xjl0PHracx47Z-AYrGX7Vx5uM3xckUu9EbaJHu08NLlflnamFJYpFAVdHoff5-_4KbyaJ2Cl1R5UM_XFZC1LWkzIzLrxedhiKQDwmajH9l1sYvdz1g=w320-h200-k',
                    info: 'ddddddddddddddd'
                },
                {
                    title: 'Auguste Renoir',
                    image: 'https://lh3.googleusercontent.com/fife/AAWUweVPgZG9dxPsXbskpftmyR0AGxQ2AqnnFwX4Sh5y9sdtGNLcpLB27RZpJOHNlCKrhmfIKaRY_Q1zVbqK5uAVYxlDNVUDYEN-FmcjrJtfrjr9Q0Lh1a3BH0_g8qjmUhGLVZsmZXnVGvPX-nXisIATv-Gthk99IJ9QUrzgbaGm-pPtURQyuR2J9Yq4dm14yiMd8ECeBxgblvr5y50eFMrfEYvP5XF816OC3y1gISltIoUBdpFYDA5R2qfltRnj5hDDrTe9gH9Ws4MgBXbSDGkZJdaaOuL86T008kOfdELHIaxYdQRf4LkGF-3KmRK9dHwZkGwWPUbI7hJkNtfUiNoBhy5XjQ5MDnEmZ_JRToznpOK0FPJXQJQPgp-VjJeyawVklzZzJXziNXq2_eiebTLxcJ0CEds6jwgxeX3-0JIiINrdBaajQ6hFhTb1SIoUcoGN21Av6kPv2taVgp_syLTJaMtS6cqkNzn7HTbGz8cGhz_qK8AozyH0BEXrakI_V-Hs9hKOSgTyuVcUEAsaQDHYxKaDZq5mfrBTEbQbmbkPjR8IlY7AF1ew40uYnrxzYST1lc6hdPHsHsA3uFW9fSPYyjDe0rUpDRZv4ZAkGOUjqYB6m4eROakbAkhY12ylzDFw5-fY9IjhxcT1LhryigXvios_Y36Ax0QMfAXL2mWJeM9CYtM9ZZFVZjsWzStMVTmJnaSx6BKmxSEB6qYwDujL611kW4bwLxoHUg=w320-h200-k',
                    info: 'eeeeeeeeeeeeeeeeeeeee'
                },
                {
                    title: 'Edgar Degas',
                    image: 'https://lh3.googleusercontent.com/fife/AAWUweUavF2177MZqWuZiNaDfKcaisp7aUJCSv42TR2GhkhkU0Tx7L75MLgDQSbxQlElD967rYaqwcNf9MjovojH0fyj-FyxTiLaJ0uUC_jHad-lNcyTFgoYRauXXfbp7_jsJVlnU6hxK65A-fAzGqCfJMgb8VWbAPgPEEuiYCXQzL2cB-5LEeYO9yRHjduuSuCwe86ehWJwAQTNWjbUlugYTIdJxREdKldub3CAZLq6YDQEc9xB7HRO8nB7VnAEu9oproTf8YRRP2h0x5_s7G1hkN76tjbkaU4Ijn4jOW9hCM0y5qCXeowhMaCM_-c5ISCOSg-z1wyMZrCTdhzjop03MhfouYoQ369Ye58TpHChE9i9xQr4JEsGVP9zQx9DRrDQ5V3AA3BYIcnK3Rb--NBVMg7aQLfo1mgkjUh4hH5cDJT9l7hvRD458MWdpi_cHHhwFwQ156zDWsqDQmo86yGcAjHwjLmo1_5cCxqtsLjSSnZjQvOO_t3HiSHl4zSc6nrvhkBqXSta11dmonQuwJMX_q7YqVt1aMbxkU3ToHugZ9VW6kyaP4t5eiAz91xIU9n47T_h_qiH6OsTb7gYkpdlDxHvDJLZ0ojpdtzgquA_7hCcjv9dzrkgFHS7t-Y_52CaEDAhgYEOrfc4v1ZbVOvJRh7kC1l_nSEw0fK1A-UllDfVjKD_rihbyMQj3R8_-esLwVb1G0hpNhhL6vG0xeLkpQBX9-FPmgCoCQ=w320-h200-k',
                    info: 'ffffffffffffff'
                },
                {
                    title: 'Berthe Morisot',
                    image: 'https://lh3.googleusercontent.com/fife/AAWUweWshMt0sHaJWN4XQuM436wn1kBSKkL1FeeLjs6-vuLwdGg4XW5QeBnQaxjOOXd28iw4nEnWFIIWwXmvhlVuRrNtWae0myJ2RN8Px9qJg8AbIiF7C5dYpjofhKfbqZk8V6I_vWk7x5C2LCpjxlhoXHzhVYSsyOO6TJJ9tX258i6sK4qwk50AMsrMkaqUqHsOQVrg-HBklCiZPOtmjkNZeTYxXTOxbWJlvagqZBDAeVrOFfX5q6G-hgSoFeUNgFxZubTWkQHb5d2WGm8j5CyytnZYTe_bBFpYaD8k8Bgvo5bMWsCDjC2tUpsbCgGva5NyNRG1qcmrO9dhZRJKwNXTH73t3ikhbC5uYQgKjvvqfV_d94klujMoF7dGJ5RJ4eOzLUcpi3UYEX1m6X_uK2KgD24nMd63Z53CnRK01keprTQ-0INtLdOz6LhvJ36vCA2Xx58_wSqZz4mcILFyVtqDSdTvu45cKT6WmHa0NIyRNYTzjB8nGsgkpstOwtLolTEphmowNnX9Uoewm8Pjr0VfxlmnnU-ys0giKXO4JoGpxdFL7wj3dpazW8qWQslJ4Z9z7JJ0C0DPCNT0TXpuU40rrNcL_uNCzHbpAwdZvj8xZodT7N3SCk9Dsm4gxgY0UeHyNmxvQvwkE_WfSSsBhpA2Gv8T7fl7GBtIyOE0gehF8NfHBpvHHStzHOU-rijY4fzfFJRuN-aNOxmNTNBqdswgpVeLCcF12E0lHQ=w320-h200-k',
                    info: 'ggggggggggggggggg'
                },
                {
                    title: 'Armand Guillaumin',
                    image: 'https://lh3.googleusercontent.com/fife/AAWUweV8bSLyvS_IcbI7xFAYXIATiJ-B7njX31pD-sRbW0V4LmmmiMrlETqFtD3OYhL1qXmil3XMm00uBQgTeggY3NxdXVMBPP1jSkqqTl_JK2lCHox5vMFDxrnjb3Fvc_PQW7SIZlpdsnJ5XphstuOWSUobprS-IC3rk__IT3NUM64vEOtoLRBvKHTSX_qd91iQd7-XVDg7Namb1BX29UeKIztAYeAzRRJUVYTDZFLstBqPiCMbQGwJkqUjA74vzX7XMLEgoYS_x3hMVgEao1sQjPxRn6v_QkvLFnXMgp4UZBjMPoAB9QrErxfS3SMiTeS4edMJhXi-rT9eg-3Llrk6KJOADEolPlbpgmVehiiSqcj0PaXAKXWqyG6fdlKDicUGHTpmudD9xhK71VE7yViiE-da7h9_2gGCD4ptwE_cQqAMd8O6cBCq_63NAFcS4glA2OnehHADXrXjBcWJRx2FZewh-uTKhZFi0uFCVl0j09iUHdAcFzeUQwXotW8xOK7_JpP9btmCkGNQjnHtRuOENMH9lJ7RGyVvM8eE_WqND0tFRfT2Nl9y3B3OMP453rsJmgcCTSc_zwt4ZSG6iLEdXMDcSK5cD4igz1f2HFaMC2atJBPkGu1E2mnVH9lO4mWM4aNiRDxfKDQz1u8oTUMtRwkEXguhhc30XidOnrXPromXhhYLH3-i7T6-ls-y5teNlLDo0KNWmz5a8WyqU7Jzq7oy7FLNLI2DSQ=w320-h200-k',
                    info: 'hhhhhhhhhhhhhhhhh'
                }
            ],
            arts:[
              {
                title:'The starry night',
                artist:'Vincent Van Gogh',
                images:'https://upload.wikimedia.org/wikipedia/commons/c/cd/VanGogh-starry_night.jpg',
                info:'《별이 빛나는 밤》은 네덜란드의 화가 빈센트 반 고흐의 가장 널리 알려진 작품이자 정신병을 앓고 있을 당시 고흐가 그린 그림이다. 1889년 생 레미의 정신병원에서 고흐는 정신적 질환으로 인한 고통을 떠올려 그림 속의 소용돌이로 묘사했다.'
              },
              {
                title:'Cafe terrace at night',
                artist:'Vincent Van Gogh',
                images:'https://upload.wikimedia.org/wikipedia/commons/0/09/Van_Gogh_-_Terrasse_des_Caf%C3%A9s_an_der_Place_du_Forum_in_Arles_am_Abend1.jpeg',
                info:'밤의 카페 테라스는 1888년 빈센트 반 고흐가 그린 그림이다. 반 고흐는 1888년 9월 중순에 프랑스 아를에서 그림을 그렸다. 그림에는 서명이 없지만 반 고흐가 세 가지 편지에서 설명하고 언급했다. 아를의 포룸 광장의 북동쪽에서 그가 그린 그림의 배경을 직접 볼 수 있다.'
              },
              {
                title:'Sunflower',
                artist:'Vincent Van Gogh',
                images:'https://upload.wikimedia.org/wikipedia/commons/b/b4/Vincent_Willem_van_Gogh_128.jpg',
                info:'《해바라기》는 빈센트 반 고흐가 그린 정물화이다. 이 그림은 두 가지 버전이 있는데, 첫 번째는 1887년 파리에서 그린 바닥에 놓여있는 해바라기이며, 두 번째는 1년 뒤 아를에서 그린 꽃병에 담긴 해바라기이다.'
              },
              {
                title:'Arles bedroom',
                artist:'Vincent Van Gogh',
                images:'https://upload.wikimedia.org/wikipedia/commons/3/3b/Vincent_Van_Gogh_0011.jpg',
                info:'아를의 침실은 1888년 고흐가 그린 그림이다. 1888년 제작되었으며 탈인상주의 근대미술이다.'
              },
              {
                title:'self-portrait',
                artist:'Vincent Van Gogh',
                images:'https://upload.wikimedia.org/wikipedia/commons/b/b2/Vincent_van_Gogh_-_Self-Portrait_-_Google_Art_Project.jpg',
                info:'네덜란드 포스트 인상파 화가 빈센트 반 고흐는 1889 년 9 월 캔버스에 유화로 자화상을 그렸습니다.이 작품은 반 고흐의 마지막 자화상 이었을지 모르지만 그가 남부의 생 레미 드 프로방스를 떠나기 직전에 그렸습니다. 프랑스. 이 그림은 현재 파리의 오르세 미술관에 있습니다.'
              },
              {
                title:'Boulevard Montmartre, soleil après-midi',
                artist:'Camille Pissarro',
                images:'https://upload.wikimedia.org/wikipedia/commons/5/5d/Pissarro_Camille_-_Boulevard_Montmartre_%C3%A0_Paris.jpg',
                info:'카미유 피사로의 74*93cm 크기 유화 그림이다. 1897년 제작되었으며 소재지는 몽마르트이다.'
              },
              {
                title:'View of the Village of Éragny',
                artist:'Camille Pissarro',
                images:'https://upload.wikimedia.org/wikipedia/commons/0/02/The_Village_of_%C3%89ragny_by_Camille_Pissarro.jpg',
                info:'카미유 피사로의 59.7*73cm의 풍경화를 그린 유화이다. 1979년에 제작되었다.'
              },
              {
                title:'the boy who plays the flute',
                artist:'Édouard Manet',
                images:'https://upload.wikimedia.org/wikipedia/commons/a/a2/Manet%2C_Edouard_-_Young_Flautist%2C_or_The_Fifer%2C_1866_%282%29.jpg',
                info:'Fifer 또는 Young Flautist는 1866 년에 만든 프랑스 화가 Édouard Manet의 그림입니다. 일반적으로 파리의 오르세 미술관에 보관되어 있습니다.'
              },
              {
                title:'The Street Singer',
                artist:'Édouard Manet',
                images:'https://upload.wikimedia.org/wikipedia/commons/c/c5/Edouard_Manet_072.jpg',
                info:'The Street Singer는 Édouard Manet이 카바레 입구 근처에있는 여성 거리 음악가를 묘사 한 1862 년 유화 캔버스입니다. 크기는 171.1 x 105.8 cm이며 보스턴 미술관에 있습니다. '
              },
              {
                title:'Lola de Valence',
                artist:'Édouard Manet',
                images:'https://upload.wikimedia.org/wikipedia/commons/5/57/Edouard_Manet_044.jpg',
                info:'마네의 그림으로 스페인 발레에 등장하는 몰라라는 발레리나를 그린 초상화이다. 스커트의 적,흑,황,녹의 대담한 채색법은 형태나 음영과의 유기적인 연관을 제일의로 삼았던 전통적인 채색법에의 반역으로 당시 평론가들에 의해 잡탕 칠이란 혹평을 받았다.'
              },
              {
                title:'The Boy in the Red Vestcoat',
                artist:'Paul Cézanne',
                images:'https://upload.wikimedia.org/wikipedia/commons/2/24/Le_Gar%C3%A7on_au_gilet_rouge%2C_par_Paul_C%C3%A9zanne%2C_FWN_496.jpg',
                info:'빨간 조끼를 입은 소년 (The Boy in the Red Vestcoat)은 1889 년 또는 1890 년에 그려진 Paul Cézanne의 그림입니다. 1880 년 이후 세잔의 숙련되고 미묘하고 혁신적인 성숙한 작품의 훌륭한 예입니다.'
              },
              {
                title:'Dance at Bougival',
                artist:'Auguste Renoir',
                images:'https://upload.wikimedia.org/wikipedia/commons/f/f9/Pierre-Auguste_Renoir_-_Suzanne_Valadon_-_Dance_at_Bougival.jpg',
                info:'Dance at Bougival은 1883년 Pierre-Auguste Renoir의 작품으로 현재 미국 매사추세츠 주 보스턴에 있는 미술관에 소장되어 있습니다.'
              },
              {
                title:'The starry night',
                artist:'Vincent Van Gogh',
                images:'https://upload.wikimedia.org/wikipedia/commons/c/cd/VanGogh-starry_night.jpg',
                info:'《별이 빛나는 밤》은 네덜란드의 화가 빈센트 반 고흐의 가장 널리 알려진 작품이자 정신병을 앓고 있을 당시 고흐가 그린 그림이다. 1889년 생 레미의 정신병원에서 고흐는 정신적 질환으로 인한 고통을 떠올려 그림 속의 소용돌이로 묘사했다.'
              },
              {
                title:'Cafe terrace at night',
                artist:'Vincent Van Gogh',
                images:'https://upload.wikimedia.org/wikipedia/commons/0/09/Van_Gogh_-_Terrasse_des_Caf%C3%A9s_an_der_Place_du_Forum_in_Arles_am_Abend1.jpeg',
                info:'밤의 카페 테라스는 1888년 빈센트 반 고흐가 그린 그림이다. 반 고흐는 1888년 9월 중순에 프랑스 아를에서 그림을 그렸다. 그림에는 서명이 없지만 반 고흐가 세 가지 편지에서 설명하고 언급했다. 아를의 포룸 광장의 북동쪽에서 그가 그린 그림의 배경을 직접 볼 수 있다.'
              },
              {
                title:'Sunflower',
                artist:'Vincent Van Gogh',
                images:'https://upload.wikimedia.org/wikipedia/commons/b/b4/Vincent_Willem_van_Gogh_128.jpg',
                info:'《해바라기》는 빈센트 반 고흐가 그린 정물화이다. 이 그림은 두 가지 버전이 있는데, 첫 번째는 1887년 파리에서 그린 바닥에 놓여있는 해바라기이며, 두 번째는 1년 뒤 아를에서 그린 꽃병에 담긴 해바라기이다.'
              },
              {
                title:'Arles bedroom',
                artist:'Vincent Van Gogh',
                images:'https://upload.wikimedia.org/wikipedia/commons/3/3b/Vincent_Van_Gogh_0011.jpg',
                info:'아를의 침실은 1888년 고흐가 그린 그림이다. 1888년 제작되었으며 탈인상주의 근대미술이다.'
              },
              {
                title:'Boulevard Montmartre, soleil après-midi',
                artist:'Camille Pissarro',
                images:'https://upload.wikimedia.org/wikipedia/commons/5/5d/Pissarro_Camille_-_Boulevard_Montmartre_%C3%A0_Paris.jpg',
                info:'카미유 피사로의 74*93cm 크기 유화 그림이다. 1897년 제작되었으며 소재지는 몽마르트이다.'
              },
              {
                title:'View of the Village of Éragny',
                artist:'Camille Pissarro',
                images:'https://upload.wikimedia.org/wikipedia/commons/0/02/The_Village_of_%C3%89ragny_by_Camille_Pissarro.jpg',
                info:'카미유 피사로의 59.7*73cm의 풍경화를 그린 유화이다. 1979년에 제작되었다.'
              },
              {
                title:'the boy who plays the flute',
                artist:'Édouard Manet',
                images:'https://upload.wikimedia.org/wikipedia/commons/a/a2/Manet%2C_Edouard_-_Young_Flautist%2C_or_The_Fifer%2C_1866_%282%29.jpg',
                info:'Fifer 또는 Young Flautist는 1866 년에 만든 프랑스 화가 Édouard Manet의 그림입니다. 일반적으로 파리의 오르세 미술관에 보관되어 있습니다.'
              },
              {
                title:'The Street Singer',
                artist:'Édouard Manet',
                images:'https://upload.wikimedia.org/wikipedia/commons/c/c5/Edouard_Manet_072.jpg',
                info:'The Street Singer는 Édouard Manet이 카바레 입구 근처에있는 여성 거리 음악가를 묘사 한 1862 년 유화 캔버스입니다. 크기는 171.1 x 105.8 cm이며 보스턴 미술관에 있습니다. '
              }
            ]
    }
  },
}
</script>
<style>
  @import url('../assets/common.css');
  .artist_slide{
    margin: 50px auto;
    width: 100%;
    max-width: 1024px;
    position: relative;
  }
  .mdi-24px.mdi:before{
    color: black;
  }
  .carousel-arrow .icon:hover{
    border: black;
  }
  .artist_link{
    display: flex;
    align-items: center;
    margin: 0!important;
  }
  .artist_link li{
    width: 24px;
    height: 24px;
    margin-right: 5px;
    border-radius: 5px;
  }
  .artist_link li:hover{
    background:#eee
  }
  .artist_link li:first-child{
    margin-top: 4px;
  }
  .artist_link li img{
    opacity: 0.6;
  }
  .title.is-6{
    font-size: 0.8rem;
  }
  .modal_img{
    background-size:contain;
    background-position: center center;
    background-repeat: no-repeat;
    background-color: black;
  }
  .modal_tit{
    font-weight: 800;
    font-size: 1.25rem;
    color: black;
  }
  .modal_artist{
    color: black;
    font-weight: 600;
    font-size: 0.9rem;
  }
  .modal_info{
    font-size: 0.8rem;
    padding: 20px 0 0;
  }
</style>
