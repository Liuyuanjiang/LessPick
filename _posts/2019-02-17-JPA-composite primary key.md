---
layout: post
title:  JPA 组合主键(composite primary key)
date:   2019-02-17 01:08:00 +0800
categories: document
tag: 教程
---


* content
{:toc}
 Spring Jpa 组合主键，可以使用Idclass 和Emeddable 两种方式实现

使用Embeddable 注解
------------------------------------

 主键类：
```bash
	@Embeddable
	public class EmployeeIdentity implements Serializable {
	    @NotNull
	    @Size(max = 20)
	    private String employeeId;
	
	    @NotNull
	    @Size(max = 20)
	    private String companyId;
	
	    public EmployeeIdentity() {
	
	    }
	
	    public EmployeeIdentity(String employeeId, String companyId) {
	        this.employeeId = employeeId;
	        this.companyId = companyId;
	    }
	
	  ...get set ...
	
	    @Override
	    public boolean equals(Object o) {
	        if (this == o) return true;
	        if (o == null || getClass() != o.getClass()) return false;
	        EmployeeIdentity that = (EmployeeIdentity) o;

	        if (!employeeId.equals(that.employeeId)) return false;

	        return companyId.equals(that.companyId);
	    }
	
	    @Override
	    public int hashCode() {
	        int result = employeeId.hashCode();
	        result = 31 * result + companyId.hashCode();
	        return result;
	    }
	}
```
entity 类 
```bash
	@Entity
	@Table(name = "employees")
	public class Employee {
	
	    @EmbeddedId
	    private EmployeeIdentity employeeIdentity;
	
	    @NotNull
	    @Size(max = 60)
	    private String name;
	
	    @NaturalId
	    @NotNull
	    @Email
	    @Size(max = 60)
	    private String email;
	
	    @Size(max = 15)
	    @Column(name = "phone_number", unique = true)
	    private String phoneNumber;
	
	    public Employee() {
	
	    }
	
	    public Employee(EmployeeIdentity employeeIdentity, String name, String email, String phoneNumber) {
	        this.employeeIdentity = employeeIdentity;
	        this.name = name;
	        this.email = email;
	        this.phoneNumber = phoneNumber;
	    }
	
	    // Getters and Setters (Omitted for brevity)
	}
```
Repository类中，后面的ID泛型使用 主键类
```bash
	@Repository
	public interface EmployeeRepository extends JpaRepository<Employee, EmployeeIdentity> {
		
	  	//使用组合主键中的某一个字段进行查询 
		List<Employee> findByEmployeeIdentityCompanyId(String companyId);
	}
```

使用Idclass
------------------------------------
	
主键类：
```bash
	public class EmployeeId implements Serializable {
	
	        private String name;
	        private String departmentName;
	        private String departmentLocation;
   
	
	}
``` 
entity类

```bash
	@Entity
	@Table(name = "Employee")
	@IdClass(EmployeeId.class)
	public class Employee {
	
	    @Id
	    @Column(name = "Name")
	    private String name;

	    @Id
	    @Column(name = "Department")
	    private String departmentName;

	    @Column(name = "Designation")
	    private String designation;

	    @Id
	    @Column(name = "DepartmentLocation")
	    private String departmentLocation;

	    @ManyToOne
	    @JoinColumns({
	            @JoinColumn(name="Department", referencedColumnName="Name",insertable = false,updatable = false),
	            @JoinColumn(name="DepartmentLocation", referencedColumnName="Location",insertable = false,updatable = false),
	    })
	    @JsonIgnore
	    private Department department;

	    @Column(name = "Salary")
	    private Double salary;
	}
```
entity 使用内部类实现

```bash
	@Entity
	@Table(name = "t_airline")
	@IdClass(Airline.AirlinePK.class)
	public class Airline {
	  @Id
	  private String startCity;
	  @Id
	  private String endCity;
	  private String name;
	
	 //get set...
	
	  @Override
	  public String toString() {
	    return "Airline [startCity=" + startCity + ", endCity=" + endCity + ", name=" + name + "]";
	  }
	
	  // 必须static的class
	  public static class AirlinePK implements Serializable {
	    private static final long serialVersionUID = -7189167162738318201L;
	    @Column(length = 3, nullable = false)
	    private String startCity;
	    @Column(length = 3, nullable = false)
	    private String endCity;
	
	    public AirlinePK() {
	    }
	
	    public AirlinePK(String startCity, String endCity) {
	      this.startCity = startCity;
	      this.endCity = endCity;
	    }
	
		//..get..set ...
	
	    @Override
	    public int hashCode() {
	      final int prime = 31;
	      int result = 1;
	      result = prime * result + ((endCity == null) ? 0 : endCity.hashCode());
	      result = prime * result + ((startCity == null) ? 0 : startCity.hashCode());
	      return result;
	    }
	
	    @Override
	    public boolean equals(Object obj) {
	      if (this == obj)
	    return true;
	      if (obj == null)
	    return false;
	      if (getClass() != obj.getClass())
	    return false;
	      AirlinePK other = (AirlinePK) obj;
	      if (endCity == null) {
	    if (other.endCity != null)
	      return false;
	      } else if (!endCity.equals(other.endCity))
	    return false;
	      if (startCity == null) {
	    if (other.startCity != null)
	      return false;
	      } else if (!startCity.equals(other.startCity))
	    return false;
	      return true;
	    }
	
	    @Override
	    public String toString() {
	      return "AirlinePK [startCity=" + startCity + ", endCity=" + endCity + "]";
	    }
	
	  }
	
	}
```

注意事项
------------------------------------
 	主键类均需要重写equals 和 hashcode 的方法。