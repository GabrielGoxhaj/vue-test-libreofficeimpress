<script setup>
import { ref } from 'vue';
import MenuLibreOfficeImpress from './components/MenuLibreOfficeImpress.vue';
import MenuIconLibreOfficeImpress from './components/MenuIconLibreOfficeImpress.vue';
import TitleBar from './components/TitleBar.vue';
import FileDropdown from './components/MenuDropdowns/FileDropdown.vue';
import ModificaDropdown from './components/MenuDropdowns/ModificaDropdown.vue';
import VisualizzaDropdown from './components/MenuDropdowns/VisualizzaDropdown.vue';
import InserisciDropdown from './components/MenuDropdowns/InserisciDropdown.vue';
import FormatoDropdown from './components/MenuDropdowns/FormatoDropdown.vue';
import DiapositivaDropdown from './components/MenuDropdowns/DiapositivaDropdown.vue';
import PresentazioneDropdown from './components/MenuDropdowns/PresentazioneDropdown.vue';
import StrumentiDiapositiva from './components/MenuDropdowns/StrumentiDiapositiva.vue';
import FinestraDropdown from './components/MenuDropdowns/FinestraDropdown.vue';
import AiutoDropdown from './components/MenuDropdowns/AiutoDropdown.vue';
import DiapositiveMenu_IlSistemaSolare from './components/IlSistemaSolare/DiapositiveMenu_IlSistemaSolare.vue';
import MenuLaterale from './components/MenuLaterale.vue';
import Nascondi from './components/Nascondi.vue';
import DocumentiRecentiDropdown from './components/MenuDropdowns/FileDropdowns/DocumentiRecentiDropdown.vue';
import DiapositivaCurrent_IlSistemaSolare from './components/IlSistemaSolare/DiapositivaCurrent_IlSistemaSolare.vue';
import DiapositiveMenu_IVA from './components/IVA/DiapositiveMenu_IVA.vue';
import Proprietà from './components/MenuLaterale/Proprietà.vue';
import Diapositive_Schema from './components/MenuLaterale/Diapositive_Schema.vue';
import DiapositiveMenu_SenzaNome1 from './components/SenzaNome1/DiapositiveMenu_SenzaNome1.vue';
import DiapositivaCurrent_SenzaNome1 from './components/SenzaNome1/DiapositivaCurrent_SenzaNome1.vue';
import DiapositivaCurrent_IVA from './components/IVA/DiapositivaCurrent_IVA.vue';
import DiapositiveMenu_SocialMediaMarketing from './components/SocialMediaMarketing/DiapositiveMenu_SocialMediaMarketing.vue';
import DiapositivaCurrent_SocialMediaMarketing from './components/SocialMediaMarketing/DiapositivaCurrent_SocialMediaMarketing.vue';

// titolo pptx
const title_pptx = ref('Senza Nome 1.pptx');
const updateTitle = (title) => {
  title_pptx.value = title;
  updateDiapositiva(1);
};

// funzioni e costanti per dinamicizzare attuale dispositiva e il massimo di diapositive per ciascun file
const diapositivaNumber = ref(1);
const maxDiapositiva = ref(1);
const updateDiapositiva = (diapositiva) => {
  diapositivaNumber.value = diapositiva;
};
const updateMaxDiapositiva = (max) => {
  maxDiapositiva.value = max;
};

// visibilità dei menu laterali alla diapositiva
const isDiapositiveMenuVisible = ref(true);
const hideDiapositiveMenu = () => {
  isDiapositiveMenuVisible.value = !isDiapositiveMenuVisible.value;
};
const isMenuLateraleVisible = ref(true);
const hideMenuLaterale = () => {
  isMenuLateraleVisible.value = !isMenuLateraleVisible.value;
};
const isSubMenuLateraleVisible = ref(false);
const showSubMenuLaterale = () => {
  isSubMenuLateraleVisible.value = !isSubMenuLateraleVisible.value
}

// funzioni e costanti per i vari dropdown del menu superiore
const showDropdown = ref(null);
const dropdownPosition = ref({ top: 0, left: 0 });
const toggleDropdown = ({ type, position }) => {
  showDropdown.value = showDropdown.value === type ? null : type;
  dropdownPosition.value = position;
};
const closeDropdown = () => {
  showDropdown.value = null;
};

// funzioni e costanti per i vari dropdown dei dropdown (submenu)
const showSubDropdown = ref(null);
const subDropdownPosition = ref({ top: 0, left: 0 });
const toggleSubDropdown = ({ type, position }) => {
  console.log(showSubDropdown.value);
  showSubDropdown.value = showSubDropdown.value === type ? null : type;
  subDropdownPosition.value = position;
};
const closeSubDropdown = () => {
  showSubDropdown.value = null;
}

</script>

<template>
  <div class="libreOfficeImpress">
    <TitleBar :title_pptx="title_pptx"/>
    <div class="menu">
      <MenuLibreOfficeImpress @toggle-dropdown="toggleDropdown"/>
      <div id="dropdownsWrapper">
        <div id="fileWrapper">
          <FileDropdown @toggle-sub-dropdown="toggleSubDropdown" v-if="showDropdown === 'File'"
            :style="{ top: dropdownPosition.top + 'px', left: dropdownPosition.left + 'px' }" />
            <!-- Dropdown di File -->
            <DocumentiRecentiDropdown v-if="showSubDropdown === 'DocumentiRecenti'"
              @update-title="updateTitle"
              @toggle-dropdown="closeDropdown"
              @toggle-sub-dropdown="closeSubDropdown"
              :style="{ top: dropdownPosition.top + 'px', left: dropdownPosition.left + 'px' }" />
        </div>
        <ModificaDropdown v-if="showDropdown === 'Modifica'"
          :style="{ top: dropdownPosition.top + 'px', left: dropdownPosition.left + 'px' }" />
        <VisualizzaDropdown v-if="showDropdown === 'Visualizza'"
          :style="{ top: dropdownPosition.top + 'px', left: dropdownPosition.left + 'px' }" />
        <InserisciDropdown v-if="showDropdown === 'Inserisci'"
          :style="{ top: dropdownPosition.top + 'px', left: dropdownPosition.left + 'px' }" />
        <FormatoDropdown v-if="showDropdown === 'Formato'"
          :style="{ top: dropdownPosition.top + 'px', left: dropdownPosition.left + 'px' }" />
        <DiapositivaDropdown v-if="showDropdown === 'Diapositiva'"
          :style="{ top: dropdownPosition.top + 'px', left: dropdownPosition.left + 'px' }" />
        <PresentazioneDropdown v-if="showDropdown === 'Presentazione'"
          :style="{ top: dropdownPosition.top + 'px', left: dropdownPosition.left + 'px' }" />
        <StrumentiDiapositiva v-if="showDropdown === 'Strumenti'"
          :style="{ top: dropdownPosition.top + 'px', left: dropdownPosition.left + 'px' }" />
        <FinestraDropdown v-if="showDropdown === 'Finestra'"
          :style="{ top: dropdownPosition.top + 'px', left: dropdownPosition.left + 'px' }" />
        <AiutoDropdown v-if="showDropdown === 'Aiuto'"
          :style="{ top: dropdownPosition.top + 'px', left: dropdownPosition.left + 'px' }" />
      </div>
      <MenuIconLibreOfficeImpress @update-title="updateTitle"/>
    </div>
    <div id="mainWrapper">

      <!-- Menu Diapositive -->
      <DiapositiveMenu_IVA v-if="isDiapositiveMenuVisible && title_pptx === 'IVA.pptx'" @update-title="updateTitle" @update-diapositiva="updateDiapositiva" @update-max-diapositiva="updateMaxDiapositiva" />
      <DiapositiveMenu_IlSistemaSolare v-if="isDiapositiveMenuVisible && title_pptx === 'Il Sistema Solare.pptx'" @update-title="updateTitle" @update-diapositiva="updateDiapositiva" @update-max-diapositiva="updateMaxDiapositiva" />
      <DiapositiveMenu_SenzaNome1 v-if="isDiapositiveMenuVisible && title_pptx === 'Senza Nome 1.pptx'" @update-title="updateTitle" @update-diapositiva="updateDiapositiva" @update-max-diapositiva="updateMaxDiapositiva" />
      <DiapositiveMenu_SocialMediaMarketing v-if="isDiapositiveMenuVisible && title_pptx === 'Social Media Marketing.pptx'" @update-title="updateTitle" @update-diapositiva="updateDiapositiva" @update-max-diapositiva="updateMaxDiapositiva" />

      <div style="display:flex; align-items: center;">
      <Nascondi @click="hideDiapositiveMenu" :style="isDiapositiveMenuVisible ? '' : 'transform: rotate(180deg); margin-right: 121.26px'"/>
      
      <!-- View della diapositiva -->
      <DiapositivaCurrent_IVA v-if="title_pptx === 'IVA.pptx'" style="max-height: 410px;" :diapositivaNumber="diapositivaNumber" />
      <DiapositivaCurrent_IlSistemaSolare v-if="title_pptx === 'Il Sistema Solare.pptx'" style="max-height: 410px;" :diapositivaNumber="diapositivaNumber" />
      <DiapositivaCurrent_SenzaNome1 v-if="title_pptx === 'Senza Nome 1.pptx'" style="max-height: 410px;" :diapositivaNumber="diapositivaNumber" />
      <DiapositivaCurrent_SocialMediaMarketing v-if="title_pptx === 'Social Media Marketing.pptx'" style="max-height: 410px;" :diapositivaNumber="diapositivaNumber" />

      <Nascondi @click="hideMenuLaterale" :style="isMenuLateraleVisible && isDiapositiveMenuVisible ? 'transform: rotate(180deg)' : isMenuLateraleVisible && !isDiapositiveMenuVisible ? 'transform: rotate(180deg); margin-left: 84.26px' : (isDiapositiveMenuVisible ? 'margin-left: 37px' : 'margin-left: 121.26px')" />
      </div>

      <!-- Wrapper Menu Laterale DX -->
      <div class="subMenuLateraleWrapper">
        <Proprietà style="display: none;" />
        <Diapositive_Schema style="display: none;" />
        <MenuLaterale v-if="isMenuLateraleVisible" />
      </div>
    </div>
    <div class="footer">
      <p class="numberDiapositiva">Diapositiva {{diapositivaNumber}} di {{maxDiapositiva}}</p>
      <img src="./assets/Impress/footer.png" />
    </div>
  </div>
</template>

<style scoped>
.libreOfficeImpress {
  width: 800px;
  height: 560px;
  background-color: #f0f0f0;
  font-family: 'Segoe UI', Tahoma, sans-serif;
}

.menu {
  background-color: #fdfdfd;
  border-bottom: 1px solid #b0b0b0;
}

.libreOfficeImpress {
  border: 1px solid black;
}

hr {
  display: block;
  margin-left: auto;
  margin-right: auto;
  margin-top: 0;
  margin-bottom: 0;
}

#mainWrapper {
  display: flex;
  flex-direction: row;
  width: 100%;
  height: 410px;
}

.footer {
  display: flex;
  margin: none;
  align-items: center;
  height: 22px;
  border-top: 1px solid #c4c4c4;
}

.numberDiapositiva {
  margin: none;
  margin-left: 7px;
  font-size: 10px;
  margin-right: 4px;
  margin-bottom: 9px;
  width: 87px;
  cursor: default;
}
</style>