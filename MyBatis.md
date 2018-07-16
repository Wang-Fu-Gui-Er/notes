#MyBatis#

<mark>指定命名空间</mark>
	
	<mapper namespace=“com.**.**.***Mapper”>
	</mapper>
<mark>原型模型</mark>
	
	<resultMap id=“BaseResultMap” type=“com.**.**.**.**Po”>//对象关系映射
		<id column=“表中字段名” property=“实体中对应属性名” jdbcType=“BIGINT”/>	//id标记主键字段
		//result标记其他字段，jdbcType指名类型
		<result column=“表中字段名” property=“实体中对应属性名” jdbcType=“TIMESTAMP”/>  
	</resultMap>
<mark>SQL片段</mark>
	
	<sql id=“Base_Column_List”> //sql片段，<include>标签通过 id 引用
		id, name, sex, address
    </sql>
<mark>查询标签</mark>  
1. id 与Mapper接口方法同名  
2. resultMap 出参类型  
3. parameterType：入参类型  

	<select id=“selectByPrimaryKey” resultMap=“BaseResultMap” parameterType=“java.lang.Long”>
		select
		<include refid=“Base_Column_List”/>
		from table_name
        where id = #{id,jdbcType=BIFINT}	#入参引用
		order by field_name desc
		limit 1
        </select>
<mark>删除标签</mark>
        
	<delete id=“” parameterType=“”>
		delete from table_name 
		where id = #{id,jdbcType=BIGINT}
		limit 1
	</delete>
<mark>插入标签</mark>  
1. useGeneratedKeys， keyProperty：把自增字段赋值到实体对应属性  
2. trim进行过滤设置，prefix前缀，suffix后缀，suffixOverrides后缀忽略  
3. if 判断，test是判断的内容
	
	<insert id=“” parameterType=“com.**.**.**Po” useGeneratedKeys=“true” keyProperty=“id”>
		insert into table_name
		<trim prefix=“(” suffix=“)” suffixOverrides=“,”>
			<if test=“name != null”>
				name
			</if>
			<if test=“sex != null”>
				sex
			</if>
			<if test=“address != null”>
				address
			</if>
		</trim>
		<trim prefix=“values (” suffix=“)” suffixOverrides=“,”>
			<if test=“name != null”>
				#{name,jdbcType=VARCHAR}
			</if>
			<if test=“sex != null”>
				#{sex,jdbcType=CHAR}
			</if>
			<if test=“address != null”>
				#{address,jdbcType=VARCHAR}
			</if>
		</trim>
	</insert>
	
<mark>批量增加</mark>  
1. collection 集合类型  
2. item 遍历元素的别名  
3. separator 每次迭代之间的分隔符  
4. index 在迭代过程中，每次迭代到的位置  
5. open 该语句以""开始  
6. close 该语句以""结束  
	
	<insert id="batchInsert" parameterType="java.util.List">
		insert into
		table_name(name,sex,address)
		values
		<foreach open="(" close=")" collection="list" item="item" index="index" separator=",">   
			#{item.name},  
			#{item.sex},
			#{item.address}
		</foreach>
	</insert>
	
<mark>修改</mark>   

	<update id="" paramterType="**.**.**Po">
		update table_name 
		<set>
			<if test="name != null">
				name = #{name,jdbcType=VARCHAR}
			</if>
			<if test="sex != null">
				sex = #{sex,jdbcType=CHAR}
			</if>
			<if test="address != null">
				address = #{address,jdbcType=VARCHAR}
			</if>
		</set>
		where id = #{id,jdbcType=BIGINT}
		limit 1
	</update>
	
<mark>parameterType</mark>  
入参类型：  
list：列表  
map：用于有多个参数的情况    
java 自定义类型：实体对象
  
    int batchUpdateInfoById(@Param("list") List<Integer> list, @Param("RoleInfo") RoleInfo roleInfo); 
    
    
    <update id="batchUpdateInfoById" parameterType="java.util.Map">  
      update table_name
      <set>
    	  name = #{RoleInfo.name},
    	  sex = #{RoleInfo.sex},
    	  address = #{RoleInfo.address}
      </set>
      where id in  
      <foreach open"(" colse=")" collection="list" index="index" separator="," item="item">
    	#{item}
      </foreach>
    </update>  


To be continued......
