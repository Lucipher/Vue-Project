<template>
    <div>
        <custom-modal :value="showcstPopup" @cancel="onClose" effect="fade">
            <div slot="modal-header" class="modal-header"><h4 class="modal-title"> {{ title }} </h4></div>

              <table class="table table-hover table-striped table-responsive table-bordered table-condensed">
                <tbody>
                    <tr><td>Sales Order Number</td>
                        <td colspan="2">
                            <Input v-model="orderNo" style="width: 330px" @on-enter="OnSearch">
                                <Select clearable  filterable
                                            :value ="getLocationId(order? order.QUOTE_NUM_PREF: '')"
                                            slot="prepend"  @on-change="onChangeLocation"
                                            placeholder="Please select a location..."  style="width:180px"
                                ><Option v-for="item in locationOptions" :value="item.value" :key="item" :label="item.label">{{ item.label }}</Option>
                                </Select>
                                <Button slot="append" icon="ios-search" @click="OnSearch"></Button>
                            </Input>
                        </td>
                    </tr>
                    <tr> <td><bs-input label="Ticket_no" type="integer"  disabled :maxlength="255" :icon="true" v-model="formData.ticket_no"></bs-input></td> 
                         <td><bs-input label="QUOTE_ID" type="integer" disabled  :maxlength="255" :icon="true" v-model="formData.QUOTE_ID"></bs-input></td>
                         <td><bs-input label="ORDER_ID" type="text" disabled   :maxlength="255" :icon="true" v-model="formData.ORDER_ID"></bs-input></td>
                        
                   </tr>
                   <tr>
                        <td><bs-input label="LOCATION" type="text" disabled  :maxlength="255" :icon="true" v-model="formData.location_name"></bs-input></td>
                       
                          <td><bs-input label="CUST_NAME" type="text" disabled   :maxlength="255" :icon="true" v-model="formData.CUST_NAME"></bs-input></td>
                        
                    </tr>
                    <tr><td colspan="2">
                             <div class="form-group">
                                 <div><label for="status">ALLOCATED USER</label></div>
                                   <Cascader v-model="cascade_state_location" :data="cascadeLocationOptions"
                                  size="large"  placeholder="Please select a Group/User..."
                                  @on-change="handleUserChange" :disabled="formData.id != ''"
                                   > </Cascader>
                             </div>
                        </td>
                        <td>
                            <div class="form-group"><div><label for="status">TYPE</label></div>
                                <Select clearable filterable v-model="formData.ticket_type_id"
                                        @on-change="onChangeType"  placeholder="Please select a Type..."   style="width:180px"  >
                                    <Option v-for="item in typeOptions" :value="item.value" :key="item" :label="item.label">{{ item.label }}</Option>
                                </Select>
                            </div>
                        </td>
                      
                        </tr>
                       <tr><td colspan="2">
                             <div class="form-group">
                                 <div><label for="status">MANAGED USER</label></div>
                                   <Cascader v-model="cascade_state_location1" :data="cascadeLocationOptions"
                                  size="large"  placeholder="Please select a Group/User..."
                                  @on-change="handleUserChange1" :disabled="formData.id != ''"
                                   > </Cascader>
                             </div>
                        </td>
                        <td>
                             <div class="form-group"><div><label for="status">STATUS</label></div>
                                <Select clearable filterable v-model="formData.status_id"
                                        @on-change="onChangeStatus"  placeholder="Please select a status..."   style="width:180px"  >
                                    <Option v-for="item in statusOptions" :value="item.value" :key="item" :label="item.label">{{ item.label }}</Option>
                                </Select>
                            </div>
                        </td>
                       
                    </tr>
                   
                  </tbody>
              </table>

             
              <bs-input label="Comments" type="textarea" :maxlength="255" :icon="true" v-model="formData.comment"></bs-input>

            <div slot="modal-footer" class="modal-footer">
                <button type="button" class="btn btn-success" @click="onClose">Cancel</button>
                <button type="button" class="btn btn-primary" @click="OnSave">Save</button>
            </div>
        </custom-modal>
<!-- add$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$ finish -edit start $$$$$$$$$$$$$$$$$$     - -->
  <custom-modal :value="showcstEditPopup" @cancel="onClose" effect="fade"> 
     <div slot="modal-header" class="modal-header"><h4 class="modal-title"> {{ title }} </h4></div>
     <table class="table table-hover table-striped table-responsive table-bordered table-condensed">
                <tbody>
                  <tr>
                      <td><bs-input label="Ticket_no" type="integer"  disabled :maxlength="255" :icon="true" v-model="formData.ticket_no"></bs-input></td> 
                      <td><bs-input label="QUOTE_ID" type="integer" disabled  :maxlength="255" :icon="true" v-model="formData.QUOTE_ID"></bs-input></td>
                      <td><bs-input label="ORDER_ID" type="text" disabled  :maxlength="255" :icon="true" v-model="formData.ORDER_ID"></bs-input></td>
                     
                  </tr>
                   <tr> 
                   </tr>
                   <tr><td colspan="2">
                             <div class="form-group">
                                 <div><label for="status">ALLOCATED USER</label></div>
                                   <Cascader v-model="cascade_state_location" :data="cascadeLocationOptions"
                                             size="large"  placeholder="Please select a Group/User..."
                                             @on-change="handleUserChange" 
                                    ></Cascader>
                             </div>
                        </td>
                        <td><div class="form-group"><div><label for="status" >TYPE</label></div>
                                <Select clearable filterable v-model="formData.ticket_type_id" placeholder="Please select a Type..."   style="width:180px"
                                        @on-change="onChangeType" :disabled="formData.id != ''" >
                                    <Option v-for="item in typeOptions" :value="item.value" :key="item" :label="item.label">{{ item.label }}</Option>
                                </Select>
                            </div>
                        </td> 
                           
                    </tr>
                    <tr><td colspan="2">
                             <div class="form-group">
                                 <div><label for="status">MANAGED USER</label></div>
                                   <Cascader v-model="cascade_state_location1" :data="cascadeLocationOptions"
                                             size="large"  placeholder="Please select a Group/User..."
                                             @on-change="handleUserChange1" 
                                   > </Cascader>
                             </div>
                        </td>
                        <td>
                        <div class="form-group"><div><label for="status">STATUS</label></div>
                                <Select clearable filterable v-model="formData.status_id"
                                        @on-change="onChangeStatus"  placeholder="Please select a status..."   style="width:180px"  >
                                    <Option v-for="item in statusOptions" :value="item.value" :key="item" :label="item.label">{{ item.label }}</Option>
                                </Select>
                        </div>
                        </td>
                           
                    </tr>
                  
                  </tbody>
              </table>
              <bs-input label="Comment" type="textarea" :maxlength="255" :icon="true" v-model="formData.comment"></bs-input>
            <div slot="modal-footer" class="modal-footer">
                <button type="button" class="btn btn-success" @click="onClose">Cancel</button>
                <button type="button" class="btn btn-primary" @click="OnSave">Save</button>
            </div>

  </custom-modal>

    </div>



    
</template>

<script>
    import Vue from 'vue'
    import { mapState } from 'vuex'
    import modal from 'vue-strap/src/Modal'
    import input from 'vue-strap/src/Input'

    export default 
    {   computed: 
        {  ...mapState({  showcstPopup: state => state.cstkt.showcstPopup,
                          showcstEditPopup: state => state.cstkt.showcstEditPopup,
                          permissionData: state=> state.permission.permissionData,
                          csticketActivityData:state=> state.cstkt.csticketActivityData,
                          user: state => state.authUser,
                          csTicketlast: state => state.csticket.csTicketlast,
                          allusers: state => state.user.userTable,
                          ticketstatustable: state => state.csticketstatus.ticketstatustable,
                       }),

            order() {  if (this.selectedOrder)  return this.selectedOrder;  else return null;  },
            locationOptions() {  if (this.csticketActivityData)  return this.csticketActivityData.locationOptions;  else return null;  },
        },
        props: {  user: {    type: Object,  default: null,  },
                  selectedOrder: {  type: Object,  default: null,  },
                  details: {  type: Object, default: null, },
               },
        data () {  return {  title: '',orderNo: '', locationOptions: [],
                             formData: {   ticket_no: '',ticket_type_id: '',status_id:'',QUOTE_ID: '',ORDER_ID: '',
                                           location_id: '',name: '',  comment: '',  id: ''  ,orderStatus: '', 
                                       allocateduseremail:'', manageduseremail:'', tktstatus:'',
                                       }, statusOptions: [], typeOptions: [], allstatus:'',alltypes:'',tkttype:'',
                              cascadeLocationOptions: [],
                              cascade_state_location: [],cascade_state_location1: [],
                             } 
                    //this form data is required in the above form during rendering
                },
        created() { console.log('/cs/crud.vue---CustomModal Component created.'); 
                    this.$store.dispatch('getLastTicket');

                    this.$store.dispatch('getAssignedLocationOptions') //---create dropdown for locations--not required
                        .then((response) => 
                             {   console.log('/cs/crud.vue--created getAssignedLocationOptions success=', response);
                                 this.setAssignedLocationOptions(response.data);
                             })
                        .catch((error) => { console.error('/cs/crud.vue-getAssignedLocationOptions error=', error);  });
                   
                    this.$store.dispatch('gettickettypetable') //---create dropdown for ticket types
                       .then((response) =>
                        { console.log('/cs/crud.vue-created gettickettypetable success=', response);
                          //this.setOrderStatusOptions(response.data);
                          this.collectTypeOptions(response.data);
                          this.alltypes=response.data;
                        })
                       .catch((error) => {  console.error('/cs/crud.vue-created gettickettypetable error=', error); });
                            
                         
                    this.$store.dispatch('getticketstatustable') //---create dropdown for ticket status
                       .then((response) =>
                        { console.log('/cs/crud.vue-created getticketstatustable success=', response);
                          this.collectStatusOptions(response.data);
                          this.allstatus=response.data;
                        })
                       .catch((error) => {  console.error('/cs/crud.vue-created getticketstatustable error=', error); });
                  
//-----------------------------------------------------------------------------
                 this.$store.dispatch('useraspergroupscascade')//----------------users
                        .then((response) => 
                        {   console.log('/csticket/crud.vue created useraspergroupscascade success=', response);
                            this.cascadeLocationOptions = response.data.groupNodes;
                         
                        })
                        .catch((error) => { console.error('/csticket/crud.vue--useraspergroupscascade error=', error);  });
                 },
        components: { 'custom-modal': modal, 'bs-input': input,   },
        mounted() { console.log('/cs/crud.vue---CustomModal Component mounted. permissionData=', this.permissionData)  },
        methods: 
           {                  
               onChangeType(val) { console.log('/OL/cscrud---onChangeType val=',val);    },
               collectTypeOptions(types) 
                     {  console.log('/cs/cscrud---collectTypeOptions types=',types);
                        let options = [];
                        for (let type in types) 
                         { options.push({value: types[type].id, label: types[type].ticket_type});  }
                           this.typeOptions = options;
                     },
               onChangeStatus(val) { console.log('/OL/cscrud---onStatusLocation val=',val);    },
               collectStatusOptions(statuses) 
                     {  console.log('/OL/cscrud---setOrderStatusOptions statuses=',statuses);
                        let options = [];
                        for (let status in statuses) 
                         { options.push({value: statuses[status].id, label: statuses[status].STATUS});  }
                           this.statusOptions = options;
                     },
               
               OnSave() 
                {  console.log('/cs/cscrud-----OnSave_click');
                    console.log('/cs/crud-----onSave:',this.formData);
                      if ( this.formData.QUOTE_ID==null)
                             {  this.$store.dispatch('showErrorNotification', 'Please search an Order');  return;
                            }
                       else if (!this.formData.group1) {this.$store.dispatch('showErrorNotification', 'Please select Allocated User');  return;}
                      else if(this.formData.group1 && this.formData.group1.id=="")
                             {  this.$store.dispatch('showErrorNotification', 'Please select Allocated User');  return;
                            }
                     else if (!this.formData.group2) {this.$store.dispatch('showErrorNotification', 'Please select Managed User');  return;}
                     else if(this.formData.group2 && this.formData.group2.id=="")
                             {  this.$store.dispatch('showErrorNotification', 'Please select Managed User');  return;
                            }
                     else if ( this.formData.ticket_type_id=="")
                             {  this.$store.dispatch('showErrorNotification', 'Please select TYPE');  return;
                            }
                       else if ( this.formData.status_id=="")
                             {  this.$store.dispatch('showErrorNotification', 'Please select Status');  return;
                            }
                           


                          var allu=this.allusers; var uu1=this.formData.user1; var uu2=this.formData.user2;
                          var allocateduseremail=''; var manageduseremail='';
                          Object.keys(allu).forEach(function(key) 
                          {  if(allu[key].id==uu1.id)
                               allocateduseremail=allu[key].email
                               if(allu[key].id==uu2.id)
                               manageduseremail=allu[key].email
                           });
                          this.formData.allocateduseremail=allocateduseremail;
                          this.formData.manageduseremail=manageduseremail;

                            var ss=this.formData.status_id;
                                var tktstatus=''; var allstatus1= this.allstatus;
                                console.log('allstatus',this.allstatus);
                                for (let status in allstatus1) 
                                    { if (allstatus1[status].id==ss)
                                        tktstatus=allstatus1[status].STATUS;
                                     }
                                console.log('tktstatus=',tktstatus);
                                this.formData.tktstatus=tktstatus;

                                var tt=this.formData.ticket_type_id;
                                var tkttype=''; var alltypes1= this.alltypes;
                                console.log('alltypes',this.alltypes);
                                for (let status in alltypes1) 
                                    { if (alltypes1[status].id==tt)
                                        tkttype=alltypes1[status].ticket_type;
                                     }
                                console.log('tkttype=',tkttype);
                                this.formData.tkttype=tkttype;
                               // return;

                    let payload = {  isShow: false,  data: this.formData, };
                    if (this.csticketActivityData.action === 'Add')// add new state
                       {    console.log('/cs/crud-----inside add');
                           
                              
                           console.log('/cs/crud-----add inside formdata:',this.formData);
                   
                            console.log('/cs/crud-----inside payload:',payload);
                            this.$store.dispatch('setCsTicketShowPopup', payload); 
                            this.$store.dispatch('addCsTicket', this.formData)
                               .then((response) => {  console.log(' save success'); 
                                                      this.$events.fire('refreshcsticket');
                                                    })
                              .catch((error) => {console.log('save error');});
                        } 
                       else if (this.csticketActivityData.action === 'Edit')// add new state
                       {    console.log('/cs/crud-----Edit formdata:',this.formData);
                            console.log('/cs/crud-----Edit payload:',payload);
                            this.$store.dispatch('setCsTicketShowPopup', payload); 
                            this.$store.dispatch('editCsTicket', this.formData)
                               .then((response) => {  console.log(' edit success'); 
                                                      this.$events.fire('refreshcsticket');
                                                    })
                               
                              .catch((error) => {console.log('save error');});
                        } 
                    else  {  console.log('/cs/crud-----error after add');   }// error
                },
          OnSearch() 
            {   console.log('/cs/crud--onSearch orderNo=', this.orderNo);
                console.log('/cs/crud--onSearch location=', this.location);
                // check validation
                if (this.isEmpty(this.orderNo))
                {   this.$store.dispatch('showErrorNotification', 'Please input the sales order number!');   return;  }
                if (!this.location)
                {   this.$store.dispatch('showErrorNotification', 'Please input the location!');   return; }
                let payload = {  orderNo: this.orderNo, location: this.location, };
                 this.$store.dispatch('getOrderOnSearchTkt', payload)
                    .then((response) => { console.log('/cs/crud.vue- getOrderDetailOnSearch response=', response);  })
                    .catch((error) =>{ console.log('/cs/crud.vue-- getOrderDetailOnSearch error=', error);   })
            },
            setAssignedLocationOptions(locations) 
            {   console.log('/cs/list.vue----setAssignedLocationOptions locations=',locations);
                let options = [];
                for (let location in locations) 
                {  options.push({ value: locations[location].id, label: locations[location].name,
                                  abbr: locations[location].abbreviation,
                                });
                }
                this.locationOptions = options;
                console.log('/cs/list.vue----setAssignedLocationOptions this.locationOptions=',this.locationOptions);
            },

           onClose() 
              {   console.log('/cs/crud.vue---onClose');
                  let payload = { isShow: false, data: this.formData, };
                  this.$store.dispatch('setCsTicketShowPopup', payload);
                  this.resetFormData();
                  
               },
            resetFormData() { this.formData = 
                                    { name: '', comment: '', id: '', 
                                      user1: {id:'', name:''},
                                      group1: {id:'', name:''}, 
                                      status_id:'', allocateduseremail:'', manageduseremail:'',
                                      ticket_type_id:'',   tktstatus:'',alltypes:'',allstatus:'',tkttype:'',
                                    };  
                              this.cascade_state_location = []; this.cascade_state_location1 = [];
                            },


            onChangeLocation(selVal) 
            {   console.log('/cs/crud.vue----onChangeLocation selVal=', selVal);
                this.location = this.getLocationAbbr(selVal);
            },
            getLocationAbbr(locationId) 
            {   let locationAbbr = '';
                if (locationId == '') return locationAbbr;
                this.locationOptions.forEach( item => 
                {   if (item.value == locationId)
                    { locationAbbr = item.abbr; }
                });
                return locationAbbr;
            },
            getLocationId(locationAbbr) 
            {   let locationId = '';
                if (locationAbbr == '') return locationId;
                this.locationOptions.forEach( item => 
                {  if (item.abbr == locationAbbr)  { locationId = item.value; }
                });
                return locationId;
            },

            handleUserChange (value, selectedData) //----change user
            {  console.log('/csticket/crud.vue--handleUserChange value=', value);
                 console.log('/csticket/crud.vue--handleUserChange selectedData=', selectedData);
                // this.formData.location = {id:'', name:''};
                // this.formData.state = {id:'', name:''};

                 this.formData.user1 = {id:'', name:''};
                 this.formData.group1 = {id:'', name:''};
                 if (selectedData.length > 0)
                   {  this.formData.group1 = {id: selectedData[0].value, name: selectedData[0].label};
                      this.formData.user1 = {id: selectedData[selectedData.length-1].value, name: selectedData[selectedData.length-1].label};
                   }
            },
           handleUserChange1 (value, selectedData) //----change user
            {  console.log('/csticket/crud.vue--handleUserChange value=', value);
                 console.log('/csticket/crud.vue--handleUserChange selectedData=', selectedData);
                // this.formData.location = {id:'', name:''};
                // this.formData.state = {id:'', name:''};

                 this.formData.user2 = {id:'', name:''};
                 this.formData.group2 = {id:'', name:''};
                 if (selectedData.length > 0)
                   {  this.formData.group2 = {id: selectedData[0].value, name: selectedData[0].label};
                      this.formData.user2 = {id: selectedData[selectedData.length-1].value, name: selectedData[selectedData.length-1].label};
                   }
            },

        },
        watch: 
        {   
            csticketinbooking()
            { console.log('/cs/crud.vue- csticketinbooking =', this.csticketinbooking); 
                if (this.csticketActivityData)
                { this.formData.QUOTE_ID=this.csticketinbooking.QUOTE_ID;
                  console.log('/cs/crud.vue- csticketinbooking =', this.formData.QUOTE_ID); 
                }
            },
            csticketActivityData(newVal, oldVal)
             {  
                console.log('/cs/CsticketCrud.vue--++++++csticketActivityData changed newVal=', newVal);
                console.log('/cs/CsticketCrud.vue--+++++csticketActivityData changed oldVal=', oldVal);
                console.log('/cs/CsticketCrud.vue--+++++csticketActivityData =', this.csticketActivityData);
                if (this.csticketActivityData && this.csticketActivityData.action === 'Add')
                {   console.log('/cs/crud.vue- inside add'); 
                    this.resetFormData();
                    var aa=this.csTicketlast.id; aa++;   aa = String(aa).trim(); 
                    this.formData.ticket_no=aa;
                    this.title = 'Adding new TICKET';
                  //  this.formData.location_id=this.csticketActivityData.loccation.id;
                    this.formData.QUOTE_ID=this.csticketActivityData.QUOTE_ID;
                    this.formData.CUST_NAME=this.csticketActivityData.CUST_NAME;
                    this.formData.ORDER_ID=this.csticketActivityData.UDF1;
                    this.formData.PRICE=this.csticketActivityData.QUOTE_VERS;
                    
                   if(this.csticketActivityData.location) 
                   { var bb =this.csticketActivityData.location.id; bb= String(bb).trim(); 
                    this.formData.location_id=bb;
                    console.log('/cs/crud.vue- this.csticketActivityData.loccation.id=', bb); 
                    this.formData.location_name=this.csticketActivityData.location.name;
                   }

                }
                else if (this.csticketActivityData && this.csticketActivityData.action === 'Edit')
                {  console.log('/cs/crud.vue- inside edit'); 
                   
                    this.resetFormData();
                    this.title = 'Edit TICKET';
                    this.formData.id = this.csticketActivityData.data.id;
                    this.formData.ticket_no = this.csticketActivityData.data.ticket_no;
                    this.formData.QUOTE_ID = this.csticketActivityData.data.QUOTE_ID;
                    this.formData.ORDER_ID = this.csticketActivityData.data.ORDER_ID;
                    this.formData.comment = this.csticketActivityData.data.comment;
                    this.formData.CUST_NAME = this.csticketActivityData.data.CUST_NAME;
                   
                   
                    this.formData.status_id = this.csticketActivityData.data.STATUS;
                    // this.formData.ticket_type_id = this.csticketActivityData.data.ttype.ticket_type;
                    this.formData.status_id = this.csticketActivityData.data.tstatus? this.csticketActivityData.data.tstatus.id : '';
                    this.formData.ticket_type_id = this.csticketActivityData.data.ttype? this.csticketActivityData.data.ttype.id : '';
                     //------------for user and ts group
                    this.formData.group1 = {  id : this.csticketActivityData.data.agroupid.id,
                                               name: this.csticketActivityData.data.agroupid.name
                                            };
                    this.formData.user1 = { id : this.csticketActivityData.data.auserid.id,
                                                name: this.csticketActivityData.data.auserid.name,
                                            };
                    this.formData.group2 = {  id : this.csticketActivityData.data.bgroupid.id,
                                               name: this.csticketActivityData.data.bgroupid.name
                                            };
                    this.formData.user2 = { id : this.csticketActivityData.data.buserid.id,
                                                name: this.csticketActivityData.data.buserid.name,
                                            };
                    this.cascade_state_location.push(this.formData.group1.id);
                    this.cascade_state_location.push(this.formData.user1.id);
                    this.cascade_state_location1.push(this.formData.group2.id);
                    this.cascade_state_location1.push(this.formData.user2.id);
                   //---------user group finished
                   this.formData.location_id=this.csticketActivityData.data.location_id;
                   console.log('/cs/crud.vue- this.csticketactivity.location_id=', this.csticketActivityData.data.location_id); 
                   console.log('/cs/crud.vue- this.formData.location_id=', this.formData.location_id); 
                   

 
                }
            }
        }
    }
</script>

<style scoped>
</style>
