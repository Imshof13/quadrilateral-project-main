<template>
    <v-container>
      <h1>Personil Jurnalisa</h1>
      <div class="pa-5 border">
        <v-table class="border border-solid text-center fixed-table">
          <thead>
            <tr>
              <th class="cell-border text-center">Ketua</th>
              <th class="cell-border text-center">Wakil Ketua</th>
              <th class="cell-border text-center">Sekretaris</th>
            </tr>
          </thead>
          <tbody>
            <tr>
                <td class="cell-border text-center">
                    <input type="file" ref="fileInputKetua" @change="handleImageUpload ('ketua')" style="display: none"/>
                    <div v-if="!imageUrlKetua" @click="triggerFileInput('ketua')" class="upload-container">
                        <v-icon large>mdi-image</v-icon>
                        <span class="add-image-text">Add Image</span>
                    </div>
                    <div v-if="imageUrlKetua" class="image-preview-wrapper" @mouseover="showRemoveIcon('ketua')" @mouseleave="hideRemoveIcon('ketua')">
                        <img v-if="imageUrlKetua" :src="imageUrlKetua" alt="Uploaded Image" class="uploaded-image" style="max-width: 100%"/>
                        <v-icon v-show="removeIconKetua" class="remove-icon" @click="removeImage('ketua')">
                            mdi-close
                        </v-icon>
                    </div>
                </td>
                <td class="cell-border text-center">
                    <input type="file" ref="fileInputWakil" @change="handleImageUpload('wakil')" style="display: none"/>
                    <div v-if="!imageUrlWakil" @click="triggerFileInput('wakil')" class="upload-container">
                        <v-icon large>mdi-image</v-icon>
                        <span class="add-image-text">Add Image</span>
                    </div>
                    <div v-if="imageUrlWakil" class="image-preview-wrapper" @mouseover="showRemoveIcon('wakil')" @mouseleave="hideRemoveIcon('wakil')">
                        <img v-if="imageUrlWakil" :src="imageUrlWakil" alt="Uploaded Image" class="uploaded-image" style="max-width: 100%"/>
                        <v-icon v-show="removeIconWakil" class="remove-icon" @click="removeImage('wakil')">
                            mdi-close
                        </v-icon>
                    </div>
                </td>
                <td class="cell-border text-center">
                    <input type="file" ref="fileInputSekre" @change="handleImageUpload('sekre')" style="display: none"/>
                    <div v-if="!imageUrlSekre" @click="triggerFileInput('sekre')" class="upload-container">
                        <v-icon large>mdi-image</v-icon>
                        <span class="add-image-text">Add Image</span>
                    </div>
                    <div v-if="imageUrlSekre" class="image-preview-wrapper" @mouseover="showRemoveIcon('sekre')" @mouseleave="hideRemoveIcon('sekre')">
                        <img v-if="imageUrlSekre" :src="imageUrlSekre" alt="Uploaded Image" class="uploaded-image" style="max-width: 100%"/>
                        <v-icon v-show="removeIconSekre" class="remove-icon" @click="removeImage('sekre')">
                            mdi-close
                        </v-icon>
                    </div>
                </td>
            </tr>
          </tbody> 
        </v-table>
        <v-row justify="end" class="mt-3">
            <v-col cols="auto">
                <v-btn class="text-white" style="background-color: #30475E;">Save</v-btn>
            </v-col>
        </v-row>    
      </div>
    </v-container>
  </template>
  
<script>
export default {
    data() {
        return {
            imageUrlKetua: null,
            imageUrlWakil: null,
            imageUrlSekre: null,
            removeIconKetua: false,
            removeIconWakil: false,
            removeIconSekre: false,
        }
    },
    methods: {
        handleImageUpload(position) {
            const fileInput = this.$refs[`fileInput${this.capitalize(position)}`]
            const file = fileInput.files[0]
            if (file) {
                const reader = new FileReader()
                reader.onload = e => {
                    this[`imageUrl${this.capitalize(position)}`] = e.target.result
                }
                reader.readAsDataURL(file)
            }
            fileInput.value = ''
        },
        triggerFileInput(position) {
            const fileInput = this.$refs[`fileInput${this.capitalize(position)}`]
            fileInput.click()
        },
        showRemoveIcon(position) {
        this[`removeIcon${this.capitalize(position)}`] = true
        },
        hideRemoveIcon(position) {
            this[`removeIcon${this.capitalize(position)}`] = false
        },
        removeImage(position) {
            this[`imageUrl${this.capitalize(position)}`] = null
            this[`removeIcon${this.capitalize(position)}`] = false
        },
        capitalize(string) {
            return string.charAt(0).toUpperCase() + string.slice(1)
        },
    },
}
</script>
  
<style scoped>
.cell-border {
    border: 1px solid #ddd;
    padding: 8px;
  }
  
thead th {
    border: 1px solid #ddd;
    padding: 8px;
  }
  
.upload-container {
    display: flex;
    align-items: center;
    justify-content: center;
    cursor: pointer;
}

.add-image-text {
    margin-left: 8px;
    color: #007FFF;
}

.uploaded-image {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    object-fit: cover;
}

.image-preview-wrapper {
    position: relative;
    width: 150px;
    padding-bottom: 150px;
    margin: 10px auto 0;
    overflow: hidden;
}

.fixed-table {
    width: 100%;
    max-width: 800px;
    margin: 0 auto;
}

.remove-icon {
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    color: black;
    cursor: pointer;
    background: rgba(0, 0, 0, 0.175);
    border-radius: 50%;
    padding: 5px;
}
</style>
  