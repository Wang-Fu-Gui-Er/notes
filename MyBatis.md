#MyBatis

<mark>指定命名空间<mark>
	
	<mapper namespace=“com.**.**.***Mapper”>
	</mapper>
<mark>原型模型<mark>
	
	<resultMap id=“BaseResultMap” type=“com.**.**.**.**Po”>//对象关系映射
		<id column=“表中字段名” property=“实体中对应属性名” jdbcType=“BIGINT”/>	//id标记主键字段
		//result标记其他字段，jdbcType指名类型
		<result column=“表中字段名” property=“实体中对应属性名” jdbcType=“TIMESTAMP”/>  
	</resultMap>
<mark>SQL片段<mark>
	
	<sql id=“Base_Column_List”> //sql片段，<include>标签通过 id 引用
		id, name, sex, address
        </sql>
<mark>查询标签<mark>  
<mark>id 与Mapper接口方法同名<mark>  
<mark>resultMap 出参类型<mark>  
<mark>parameterType：入参类型<mark>  
<mark><mark>

	<select id=“selectByPrimaryKey” resultMap=“BaseResultMap” parameterType=“java.lang.Long”>
		select
		<include refid=“Base_Column_List”/>
		from table_name
                 where id = #{id,jdbcType=BIFINT}	#入参引用
		order by field_name desc
		limit 1
        </select>
<mark>删除标签<mark>
        
	<delete id=“” parameterType=“”>
		delete from table_name 
		where id = #{id,jdbcType=BIGINT}
		limit 1
	</delete>
<mark>插入标签<mark>
	
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
	