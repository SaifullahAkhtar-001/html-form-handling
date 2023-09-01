<template>
    <div class="flex min-h-full flex-col justify-center px-6 py-12 lg:px-8">
        <div class="sm:mx-auto sm:w-full sm:max-w-sm">
            <img class="mx-auto h-16 w-auto" src="./../assets/s.png" alt="Your Company">
            <h2 class="mt-10 text-center text-2xl font-bold leading-9 tracking-tight text-white">Sign in to your account
            </h2>
        </div>

        <div class="mt-10 sm:mx-auto sm:w-full sm:max-w-sm">
            <form class="space-y-6" @submit.prevent="validateData">
                <div>
                    <label
                        class="font-semibold flex item-center justify-start text-sm font-medium leading-6 text-white">Email
                        address</label>
                    <div class="mt-2">
                        <input type="email" required v-model="email"
                            class="block w-full rounded-md border-0 py-1.5 px-2 text-slate-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6">
                    </div>
                </div>

                <div>
                    <div class="flex items-center justify-between">
                        <label class="font-semibold block text-sm font-medium leading-6 text-white">Password</label>
                    </div>
                    <div class="mt-2">
                        <input type="password" :class="{ 'border-red-500 border-2': passwordErr }" required v-model="password"
                            class="block w-full rounded-md py-1.5 px-2 text-slate-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6">
                        <p v-if="passwordErr" class="flex items-center justify-between text-red-600">{{ passwordErr }}</p>
                    </div>
                </div>

                <div>
                    <div class="flex items-center justify-between">
                        <label class="font-semibold block text-sm font-medium leading-6 text-white">Skills</label>
                    </div>
                    <div class="mt-2">
                        <input type="text" v-model="tempSkills" placeholder="Press Enter to Add Skill" @keyup="addSkills"
                            class="block w-full rounded-md border-0 py-1.5 px-2 text-slate-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6">
                        <div v-for="skill in skills" :key="skill" @click="delSkills(skill)"
                            class="mt-4 inline-flex ml-4 cursor-pointer py-1.5 px-6 rounded-full text-white bg-white bg-opacity-5">
                            {{ skill }}
                        </div>
                    </div>
                </div>

                <div>
                    <div class="flex items-center justify-between">
                        <label for="Role" class="font-semibold block text-sm font-medium leading-6 text-white">Role:</label>
                    </div>
                    <div class="mt-2">
                        <select required v-model="role"
                            class="block w-full rounded-md border-0 py-2 px-2 font-semibold text-gray-700 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6">
                            <option value="developer">Developer</option>
                            <option value="designer">Web Designer</option>
                        </select>
                    </div>
                </div>

                <div>
                    <button type="submit"
                        class="flex w-full justify-center rounded-md bg-indigo-600 px-3 py-1.5 text-sm font-semibold leading-6 text-white shadow-sm hover:bg-indigo-500 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600">Sign
                        in</button>
                </div>
            </form>
        </div>
    </div>
    <div>
        <!-- test the fields input -->
        <p class="text-green-500 mt-4">Email:{{ email }}</p>
        <p class="text-green-500 mt-4">Password:{{ password }}</p>
        <p class="text-green-500 mt-4">Role: {{ role }}</p>

    </div>
</template>

<script>
export default {
    data() {
        return {
            email: '',
            password: '',
            role: 'designer',
            skills: [],
            tempSkills: '',
            passwordErr: ''
        }
    },
    methods: {
        addSkills(e) {
            if (e.key === ' ' && this.tempSkills) {
                this.tempSkills = this.tempSkills.replace(/,+$/, '')
                if (!this.skills.includes(this.tempSkills)) {
                    this.skills.push(this.tempSkills)
                }
                this.tempSkills = ''
            }
        },
        delSkills(skill) {
            this.skills = this.skills.filter((item) => {
                return skill !== item
            })
        },
        validateData() {
            this.passwordErr = this.password.length > 5 ? '' : 'The password must be greater than 5 characters'
            if (!this.passwordErr) {
                console.log(this.email)
            }
        }
    }
}
</script>

<style></style>