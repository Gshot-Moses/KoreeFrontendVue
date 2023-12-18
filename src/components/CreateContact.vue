


async submitEmployee() {
    try {
      if (!this.isEditing) {
        await this.$http
          .post(`http://127.0.0.1:8000/api/employees/`, {
            fullname: this.fullname,
            dep: this.dep,
            birthdate: this.birthdate,
            salary: this.salary,
          })
          .then((response) => {
            this.employees.push(response.data);
            this.fullname = "";
            this.dep = "";
            this.birthdate = "";
            this.salary = "";
          });
      } else {
        await this.$http
          .put(`http://127.0.0.1:8000/api/employees/${this.id}/`, {
            fullname: this.fullname,
            dep: this.dep,
            birthdate: this.birthdate,
            salary: this.salary,
          })
          .then((response) => {
            let objIndex = this.employees.findIndex((s) => s.id === this.id);
            let tmp = this.employees;
            tmp[objIndex] = response.data;
            this.employees = tmp;
            this.fullname = "";
            this.dep = "";
            this.birthdate = "";
            this.salary = "";
            this.id = "";
            this.isEditing = false;
            this.getEmployee();
          });
      }
    } catch (error) {
      console.log(error);
    }
},