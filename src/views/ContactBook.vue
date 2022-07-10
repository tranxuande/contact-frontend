<script>
import InputSearch from "@/components/InputSearch.vue";
import ContactList from "@/components/ContactList.vue";
import ContactCard from "@/components/ContactCard.vue";
import contactService from "@/services/contact.service.js";
export default {
    components: {
        InputSearch,
        ContactList,
        ContactCard,
    },
    data() {
        return {
            contacts: [],
            activeIndex: -1,
            searchText: "",
        };
    },
    methods: {
        async retrieveContacts() {
            try {
            this.contacts = await contactService.getAll();
        } catch (error) {
            console.log(error);
        }
     },
     refreshList() {
        this.retrieveContacts();
        this.activeIndex = -1;
     },
    },
    mounted() {
        this.refreshList();
    }
};
</script>

<template>
    <div class="page row">
        <div class="col-md-10">
        <InputSearch />
        </div>
    </div>
    <div class="mt-3 col-md-6">
        <h4>
            Danh bạ
            <i class="fas fa-address-book"></i>
        </h4>
        <ContactList 
            :contacts="contacts" 
            v-model:activeindex="activeIndex"/>
    </div> 
</template>

<style scoped>
    .page {
        text-align: left;
        max-width: 750px;
    }
</style>