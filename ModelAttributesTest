<?php

namespace Tests\Feature;

use Tests\TestCase;

class ModelAttributesTest extends TestCase
{

    /**
     * How many items test goes through
     * null == all rows in db
     * @var int|null
     */
    public $limit = 100;

    /**
     * Are the items picked in random order
     * @var boolean
     */
    public $inRandomOrder = true;

    /**
     * Get the models for testing
     *
     * @return array
     */
    protected function modelsForTesting() 
    {
        return [
            // 'App\Model',
        ];
    }

    /**
     * Test all attributes/mutators of all models
     *
     * @return void
     */
    public function test_attributes_of_the_model()
    {
        $models = $this->modelsForTesting();

        foreach($models as $model) {
            
            $methods = $model::getMutatorMethods($model);
            
            $model = $this->applyQueries($model);

            $items = is_string($model) ? $model::get() : $model->get();

            foreach($items as $item) {

                $this->tryMethods($item, $methods);

            }
        }
        $this->assertTrue(true);
    }

    /**
     * Try to call the methods
     *
     * @return void
     */
    protected function tryMethods($item, $methods) 
    {
        foreach($methods as $method) {
            try {
                $item->$method;
            } catch (\Exception $e) {
                $this->assertFalse('Method: ' . $method . ' is not working for model with id: ' . $item->id);
                break;
            }
        }
    }

   /**
     * Apply the queries
     *
     * @return void
     */
    protected function applyQueries($model) 
    {
        if(!is_null($this->limit)) {
            $model = is_string($model) ? $model::limit($this->limit) : $model->limit($this->limit);
        }

        if($this->inRandomOrder === true) {
            $model = is_string($model) ? $model::inRandomOrder() : $model->inRandomOrder();
        }

        return $model;

    }

}
